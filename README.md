import java.io.*;
import java.util.*;

// ================= CÂU 1 =================
interface IStudent {
    void work();
    void study();
}

abstract class Person {
    String name;
    private int tuoi;
    protected String id;
    public String birthDate;

    public Person(String name, int tuoi, String id, String birthDate) {
        this.name = name;
        this.tuoi = tuoi;
        this.id = id;
        this.birthDate = birthDate;
    }

    public int getTuoi() {
        return tuoi;
    }

    public void setTuoi(int tuoi) {
        this.tuoi = tuoi;
    }

    abstract void showInfo();
}

class NEUStudent extends Person implements IStudent {
    protected String studentID;

    public NEUStudent(String name, int tuoi, String id, String birthDate, String studentID) {
        super(name, tuoi, id, birthDate);
        this.studentID = studentID;
    }

    @Override
    void showInfo() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + getTuoi());
        System.out.println("ID: " + id);
        System.out.println("Birth Date: " + birthDate);
        System.out.println("Student ID: " + studentID);
    }

    @Override
    public void work() {
        System.out.println("I'm working as a student assistant.");
    }

    @Override
    public void study() {
        System.out.println("I'm studying at the university.");
    }
}

// ================= CÂU 3 =================
class Thread1 extends Thread {
    public void run() {
        int sum = 0;
        for (int i = 1; i <= 1000; i++) sum += i;
        System.out.println("Thread 1 - Tổng từ 1 đến 1000: " + sum);
    }
}

class Thread2 extends Thread {
    public void run() {
        System.out.println("Thread 2 - Số >100 và <1000:");
        for (int i = 101; i < 110; i++) { // in ít cho gọn
            System.out.print(i + " ");
        }
        System.out.println("...");
    }
}

// ================= MAIN =================
public class Main {
    public static void main(String[] args) {

        // ===== CÂU 1 =====
        System.out.println("===== CAU 1 =====");
        NEUStudent s1 = new NEUStudent("John Doe", 20, "12345", "2004-01-01", "NEU123");
        NEUStudent s2 = new NEUStudent("Jane Doe", 22, "67890", "2002-03-15", "NEU456");

        s1.showInfo();
        s1.work();
        s1.study();

        System.out.println();

        s2.showInfo();
        s2.work();
        s2.study();

        // ===== CÂU 2 =====
        System.out.println("\n===== CAU 2 =====");

        try {
            // Ghi file
            FileOutputStream fos = new FileOutputStream("raw.txt");
            fos.write("Hello world!".getBytes());
            fos.close();

            // Đọc file + in hoa
            FileInputStream fis = new FileInputStream("raw.txt");
            int ch;
            while ((ch = fis.read()) != -1) {
                System.out.print(Character.toUpperCase((char) ch));
            }
            fis.close();

        } catch (IOException e) {
            e.printStackTrace();
        }

        // ===== CÂU 3 =====
        System.out.println("\n\n===== CAU 3 =====");
        Thread1 t1 = new Thread1();
        Thread2 t2 = new Thread2();

        t1.start();
        t2.start();

        // ===== CÂU 4 =====
        System.out.println("\n===== CAU 4 =====");

        int n = 100000; // giảm để chạy nhanh
        ArrayList<Integer> arr = new ArrayList<>();
        LinkedList<Integer> link = new LinkedList<>();

        long start = System.currentTimeMillis();
        for (int i = 0; i < n; i++) arr.add(i);
        long end = System.currentTimeMillis();
        System.out.println("ArrayList add: " + (end - start) + " ms");

        start = System.currentTimeMillis();
        for (int i = 0; i < n; i++) link.add(i);
        end = System.currentTimeMillis();
        System.out.println("LinkedList add: " + (end - start) + " ms");

        start = System.currentTimeMillis();
        arr.remove(0);
        end = System.currentTimeMillis();
        System.out.println("ArrayList remove first: " + (end - start) + " ms");

        start = System.currentTimeMillis();
        link.remove(0);
        end = System.currentTimeMillis();
        System.out.println("LinkedList remove first: " + (end - start) + " ms");

        // ===== CÂU 5 =====
        System.out.println("\n===== CAU 5 =====");

        List<Integer> list = Arrays.asList(10, 5, 8, 20, 3, 15, 7, 12);

        Optional<Integer> max = list.stream().max(Integer::compare);
        Optional<Integer> min = list.stream().min(Integer::compare);

        System.out.println("Max: " + max.orElse(null));
        System.out.println("Min: " + min.orElse(null));
    }
}
