Download Spring STS and extract the archive
===========================================
C:\Software Downloads\SpringSTS\sts-bundle\sts-3.8.3.RELEASE

New -> Spring Starter Project -> "course-data-api" -> Select Web, JPA, Apache Derby
  
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

@RestController for the class
@RequestMapping for the method with the url mapping information - @RequestMapping(name="/topics")


Resources for Topics:

	GET		/topics		Gets all topics
	GET		/topics/id	Gets the topic
	POST	/topics		Create new topic
	PUT		/topics/id	Updates the topic
	DELETE	/topics/id	Deletes the topic

Topic
=====
	id
	name
	description

	@Entity
	public class Topic {

	@Id
	private String id;

TopicController
===============
	@RestController
	public class TopicController {

		@Autowired
		private TopicService topicService;

			GET		/topics		Gets all topics
			@RequestMapping(value="/topics")
				
			GET		/topics/id	Gets the topic
			@RequestMapping(value="/topics/{id}")
			public Topic getTopic(@PathVariable String id) {
				
			POST	/topics		Create new topic
			@RequestMapping(method=RequestMethod.POST, value="/topics")
			public void addTopic(@RequestBody Topic topic) {
			
			PUT		/topics/id	Updates the topic
			@RequestMapping(method=RequestMethod.PUT, value="/topics/{id}")
			public void updateTopic(@RequestBody Topic topic, @PathVariable String id) {
				
			DELETE	/topics/id	Deletes the topic
			@RequestMapping(method=RequestMethod.DELETE, value="/topics/{id}")
			public void deleteTopic(@PathVariable String id)

TopicRepository
===============
Create a repository that extends CRUD repository to use appropriate methods in that interface
	
	public interface TopicRepository extends CrudRepository<Topic, String> {


TopicService
============
	Use appropriate methods in the repository
	
	Get all	: topicRepository.findAll().forEach(topics :: add);
	Get		: return topicRepository.findOne(id);
	Add		: topicRepository.save(topic);
	Update	: topicRepository.save(topic);
	Delete	: topicRepository.delete(id);		

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

@RestController for the class
@RequestMapping for the method with the url mapping information - @RequestMapping(name="/topics/{topicId}/courses/{id}")


Resources for Courses:

	GET		/topics/topicId/courses				Gets all courses in this topic
	GET		/topics/topicId/courses/id			Gets the course in this topic
	POST	/topics/topicId/courses				Create new course under this topic
	PUT		/topics/topicId/courses/id			Updates the course 
	DELETE	/topics/topicId/courses/id			Deletes the course

Course
======
	id
	name
	description
	topic

	@Entity
	public class Course {

	@Id
	private String id;

	@ManyToOne
	private Topic topic;

CourseController
===============
	@RestController
	public class CourseController {

		@Autowired
		private CourseService courseService;

			GET		/topics/{topicId}/courses		Gets all courses in this topic
			@RequestMapping(value="/topics/{topicId}/courses")
			public List<Course> getAllCourses(@PathVariable String topicId) {
				
			GET		/topics/topicId/courses/id		Gets the course in this topic
			@RequestMapping(value="/topics/{topicId}/courses/{id}")
			public Course getCourse(@PathVariable String id) {
				
			POST	/topics/topicId/courses			Create new course under this topic
			@RequestMapping(method=RequestMethod.POST, value="/topics/{topicId}/courses")
			public void addCourse(@RequestBody Course course, @PathVariable String topicId) {
			
			PUT		/topics/topicId/courses/id		Updates the course
			@RequestMapping(method=RequestMethod.PUT, value="/topics/{topicId}/courses/{id}")
			public void updateCourse(@RequestBody Course course, @PathVariable String topicId) {
				
			DELETE	/topics/topicId/courses/id		Deletes the course
			@RequestMapping(method=RequestMethod.DELETE, value="/topics/{topicId}/courses/{id}")
			public void deleteCourse(@PathVariable String id)

CourseRepository
===============
Create a repository that extends CRUD repository to use appropriate methods in that interface
	
	public interface CourseRepository extends CrudRepository<Course, String> {

Add another method findByTopicId - just declare no implementation needed
findBy Topic Id

CourseService
============
	Use appropriate methods in the repository
	
	Get all	: courseRepository.findByTopicId(topicId).forEach(courses :: add);
	Get		: return courseRepository.findOne(id);
	Add		: courseRepository.save(course);
	Update	: courseRepository.save(course);
	Delete	: courseRepository.delete(id);		

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

@RestController for the class
@RequestMapping for the method with the url mapping information - @RequestMapping(name="/topics/{topicId}/courses/{courseId}/lessons/{id}")


Resources for Lessons:

	GET		/topics/topicId/courses/courseId/lessons		Gets all courses in this topic
	GET		/topics/topicId/courses/courseId/lessons/id		Gets the course in this topic
	POST	/topics/topicId/courses/courseId/lessons		Create new course under this topic
	PUT		/topics/topicId/courses/courseId/lessons/id		Updates the course 
	DELETE	/topics/topicId/courses/courseId/lessons/id		Deletes the course

Lesson
======
	id
	name
	description
	course

	@Entity
	public class Lesson {

	@Id
	private String id;

	@ManyToOne
	private Course course;

LessonController
===============
	@RestController
	public class LessonController {

		@Autowired
		private LessonService LessonService;

			GET		/topics/topicId/courses/courseId/lessons		Gets all lessons in this course
			@RequestMapping(value="/topics/{topicId}/courses/{courseId}/lessons")
			public List<Lesson> getAllLessons(@PathVariable String topicId) {
				
			GET		/topics/topicId/courses/courseId/lessons/id		Gets the lesson in this course
			@RequestMapping(value="/topics/{topicId}/courses/{courseId}/lessons/{id}")
			public Lesson getLesson(@PathVariable String id) {
				
			POST	/topics/topicId/courses/courseId/lessons		Create new lesson under this course
			@RequestMapping(method=RequestMethod.POST, value="/topics/{topicId}/courses/{courseId}/lessons")
			public void addLesson(@RequestBody Lesson lesson, @PathVariable String courseId) {
			
			PUT		/topics/topicId/courses/courseId/lessons/id		Updates the lesson
			@RequestMapping(method=RequestMethod.PUT, value="/topics/{topicId}/courses/{courseId}/lessons/{id}")
			public void updateLesson(@RequestBody Lesson lesson, @PathVariable String courseId) {
				
			DELETE	/topics/topicId/courses/courseId/lessons/id		Deletes the lesson
			@RequestMapping(method=RequestMethod.DELETE, value="/topics/{topicId}/courses/{courseId}/lessons/{id}")
			public void deleteLesson(@PathVariable String id)

LessonRepository
===============
Create a repository that extends CRUD repository to use appropriate methods in that interface
	
	public interface LessonRepository extends CrudRepository<Lesson, String> {

Add another method findByCourseId - just declare no implementation needed
findBy Course Id

LessonService
============
	Use appropriate methods in the repository
	
	Get all	: lessonRepository.findByCourseId(courseId).forEach(lessons :: add);
	Get		: return lessonRepository.findOne(id);
	Add		: lessonRepository.save(lesson);
	Update	: lessonRepository.save(lesson);
	Delete	: lessonRepository.delete(id);		


++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
Goto the workspace and run the maven build to create jar file
> mvn clean install

For windows
> mvnw clean install

Execute the jar to run this as a standalone application
> java -jar target/course-data-api-0.0.1-SNAPSHOT.jar

If war file is needed, then in pom.xml change <packaging> to war and run maven build to create war file

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
While using Initialize, we can also include actuator to monitor the application

	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-actuator</artifactId>		
	</dependency>

	
http://localhost:8080/health gives:
{"status" : "UP"}

In application.properties, use management.port to run actuator on a different port	
	management.port=9080
	
	http://localhost:9080/health

Some actuator endpoints are authorization restricted. To see them all, set the below property in application.properties
	management.security.enabled=false
 