import java.io.*;

public class StudentSerializationExample {

    // Serialization method
    public static void serializeStudent(Student student, String filename) {
        try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream(filename))) {
            out.writeObject(student);
            System.out.println("Student object serialized successfully.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    // Deserialization method
    public static Student deserializeStudent(String filename) {
        try (ObjectInputStream in = new ObjectInputStream(new FileInputStream(filename))) {
            Student student = (Student) in.readObject();
            System.out.println("Student object deserialized successfully.");
            return student;
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
        return null;
    }

    public static void main(String[] args) {
        // Creating a student object
        Student student = new Student("John Doe", 20, 123);

        // Serializing the student object to a file
        String filename = "student.ser";
        serializeStudent(student, filename);

        // Deserializing the student object from the file
        Student deserializedStudent = deserializeStudent(filename);

        // Display the deserialized student object
        if (deserializedStudent != null) {
            System.out.println("Deserialized Student: " + deserializedStudent);
        }
    }
}
