# LinkedList


// Define a Course class
class Course:
    courseNumber: String
    name: String
    prerequisites: Vector<String>

// Function to load courses from a file into a vector
Function loadCourses(filename: String) -> Vector<Course>:
    courses = Vector<Course>()
    file = open(filename, 'r')
    for line in file:
        tokens = line.split(',')
        course = Course(tokens[0], tokens[1], tokens[2:])
        courses.append(course)
    file.close()
    return courses

// Function to validate the courses
Function validateCourses(courses: Vector<Course>) -> Boolean:
    for course in courses:
        for prerequisite in course.prerequisites:
            if not any(c.courseNumber == prerequisite for c in courses):
                return False
    return True

// Function to find a course by its number
Function findCourse(courses: Vector<Course>, courseNumber: String) -> Course:
    for course in courses:
        if course.courseNumber == courseNumber:
            return course
    return None

// Function to print course information
Function printCourseInformation(course: Course):
    print("Course Number:", course.courseNumber)
    print("Name:", course.name)
    if course.prerequisites:
        print("Prerequisites:", ', '.join(course.prerequisites))
    else:
        print("Prerequisites: None")

// Main program
courses = loadCourses("courses.txt")
if validateCourses(courses):
    courseNumber = input("Enter a course number to get information: ")
    course = findCourse(courses, courseNumber)
    if course:
        printCourseInformation(course)
    else:
        print("Course not found.")
else:
    print("Invalid course data.")
