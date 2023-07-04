# Defination of Domain 

- We are building an application for dumping image. 
- Define a class `Image` containing features as: 
    - id
    - name
    - Image Object
- Define an `interface` like: 
    ```java
    public interface ImageRepository extends PagingAndSortingRepository<Image, Long>{
        public Image findByName(String name);
        
    }    
    ```
## Query Options 

Below are the extended queries of CrudRepository: 

```java
interface EmployeeRepository extends CRudRepository<Employee, Long>{
    
    List<Employee> findByLastName(String f)

    List<Employee> findByFirstAndLastName(String f, String l)

    List<Employee> findByFirstNameAndManagerName(String f, String m)

    List<Employee> findTop10ByFirstName(...) // or findFirst10ByFirstName

    List<Employee> findDistinctEmployeesByFirstName(...)

    List<Employee> findByFirstNameAndLastNameAllIgnoreCase(...)

    List<Employee> findByFirstNameOrderByLastNameAsc(...)

    List<Employee> findByLastNameIsNull(...)

}
```

Advanced Query Options:

```java
interface CoolRepo extends CrudRepository<Employee, Long>{
    
    Stream<Employee> findByLastname(String lastname);
    
    @Async Future<Employee> findByLastname(...)

    @Async CompletableFuture<Employee> findByLastname(...)

    @Async ListenableFuture<Employee> findByLastname(...)

    Page<Employee> findAll(Pageable p)
    Page<Employee> findByFirstName(String f, Pageable p);
    List<Employee> findAll(Sort s);
    Page<Employee> findByFirstName(String f, Pageable p, Sort s)

}
```
# Defining a File Upload Service

Inside the main package file, add a class `ImageService`

```java
@Service
public class ImageService{

    private static UPLOAD_ROOT = "upload_dir";

    private final ImageRepository repository;
    private final ResourceLoader resourceLoader;

    @Autowired
    public ImageService(ImageRepository repository, ResourceLoader resourceLoader){
        this.repository = repository;
        this.resourceLoader = resourceLoader;
    }

    public Resource findOneImage(String filename){
        return resourceLoader.getResource("file:"+UPLOAD_ROOT+"/"+filename);
    }

    public void createImage(Multipart file) throws IOException{
        if(!file.isEmpty()){
            Files.copy(file.getInputStream(), Paths.get(UPLOAD_ROOT, file.getOriginalFilename()));
            repository.save(new Image(file.getOriginalFilename()));
        }
    }

    public void deleteImage(String filename) throws IOException{
        final Image byName = repository.findBYName(filename);
        repository.delete(byName);
        Files.deleteIfExists(Paths.get(UPLOAD_ROOT, filename));
    }

    @Bean
    CommandLineRunner setUp(ImageRepository repository) throws IOException{
    return (args) -> {
            FileSystemUtils.deleteRecursively(new File(UPLOAD_ROOT));
        
            Files.createDirectory(Paths.get(UPLOAD_ROOT));
        
            FileCopyUtils.copy("Test file", new FileWriter(UPLOAD_ROOT+"/test"));
            repository.save(new Image("test"));

            FileCopyUtils.copy("Test file2", new FileWrite(UPLOAD_ROOT+"/test2"));
            repository.save(new Image("test2"));

            FileCopyUtils.copy("Test file3"), new FileWrite(UPLOAD_ROOT+"/test3"));
            repository.save(new Image("test3"));
        };
    }
}
```

# Defining the Controller

Defining a class `HomeController` for our application.

```java
@Controller
public class HomeController{
    
    private static final String BASE_PATH = "/images";
    private static final String FILENAME= "{filename:.+}";

    // using the defined service here 
    @Autowired
    public HomeController(ImageService imageService){
        this.imageService = imageService;
    }

    @RequestMapping(method = RequestMethod.GET, value = BASE_PATH + "/" + FILENAME + "/raw")
    @ResponseBody
    public ResponseEntity<?> oneRawImage(@PathVariable String filename){
        try{
            Resource file = imageService.findOneImage(filename);
                return ResposeEntity.ok()
                    .contentLength(file.contentLength())
                    .contentType(MediaType.IMAGE_JPEG)
                    .body(new InputStreamResource(file.getInputStream()));
            } catch(IOException e){
                return ResponseEntity.badRequest()
                    .body("Couldn't find" + filename + "=>" + e.getMessage()); 
            }
        }
    }
}
```

- Code to upload a file to our server
    ```
    curl -v -x POST -f file=@file/location localhost:8080/images
    ```
- Code to delete a file in our server
    ```
    curl -v -x DELETE localhost:8080/images/filename
    ```
