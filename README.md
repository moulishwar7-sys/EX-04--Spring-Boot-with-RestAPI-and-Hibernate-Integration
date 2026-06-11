# Exp-04-Spring-Boot-with-REST-API-and-Hibernate-Integration
## NAME : MOULISHWAR G
## REGISTER NO : 2305001020

## AIM:
To develop a Spring Boot application to store and retrieve data from a Movies database using Object Relational Mapping (ORM) with Hibernate and expose it via REST APIs.

## ALGORITHM:
Create Spring Boot project with dependencies:

Spring Web

Spring Data JPA

H2 or MySQL Database

Configure application.properties with DB connection and JPA settings.

Create Movie entity with fields like id, title, genre, rating, and year.

Create MovieRepository interface extending JpaRepository.

Create MovieController to define REST endpoints for CRUD operations:

GET /movies

GET /movies/{id}

POST /movies

PUT /movies/{id}

DELETE /movies/{id}


## PROGRAM CODE (Main Files):
### application.properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
### Movie.java

@Entity
public class Movie {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String title;
    private String genre;
    private int year;
    private double rating;

    // Getters and Setters
}
### MovieRepository.java
java
Copy
Edit
public interface MovieRepository extends JpaRepository<Movie, Long> {}
### MovieController.java
@RestController
@RequestMapping("/movies")
public class MovieController {
    @Autowired
    private MovieRepository repo;

    @GetMapping
    public List<Movie> getAllMovies() {
        return repo.findAll();
    }

    @GetMapping("/{id}")
    public ResponseEntity<Movie> getMovieById(@PathVariable Long id) {
        return repo.findById(id)
                .map(ResponseEntity::ok)
                .orElse(ResponseEntity.notFound().build());
    }

    @PostMapping
    public Movie addMovie(@RequestBody Movie movie) {
        return repo.save(movie);
    }

    @PutMapping("/{id}")
    public ResponseEntity<Movie> updateMovie(@PathVariable Long id, @RequestBody Movie movieDetails) {
        return repo.findById(id).map(movie -> {
            movie.setTitle(movieDetails.getTitle());
            movie.setGenre(movieDetails.getGenre());
            movie.setYear(movieDetails.getYear());
            movie.setRating(movieDetails.getRating());
            return ResponseEntity.ok(repo.save(movie));
        }).orElse(ResponseEntity.notFound().build());
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteMovie(@PathVariable Long id) {
        return repo.findById(id).map(movie -> {
            repo.delete(movie);
            return ResponseEntity.ok().build();
        }).orElse(ResponseEntity.notFound().build());
    }
}


## OUTPUT:

<img width="786" height="505" alt="image" src="https://github.com/user-attachments/assets/100a46e8-90ce-4bd7-9ed5-21a055aba7c8" />

<img width="785" height="512" alt="image" src="https://github.com/user-attachments/assets/7cd5ea86-eff8-429b-ba85-940f54636056" />

<img width="783" height="510" alt="image" src="https://github.com/user-attachments/assets/12274bdf-0048-4ca0-93df-b3941f94cf96" />

<img width="780" height="510" alt="image" src="https://github.com/user-attachments/assets/0dba04b4-53c5-49da-86fa-1d09a3a19cb0" />

## RESULT :

Thus the development of a Spring Boot application to store and retrieve data from a Movies database is completed successfully

