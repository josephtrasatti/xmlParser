import java.util.*;
import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;

public class parser {
    public static Object getValue(FileInputStream fis) {
        try {
            char current;
            current = (char) fis.read();
            if (current != '\n') {
                String value = "";
                while (current != '<') {
                    value += current;
                    current = (char) fis.read();
                }
                return value;
            } else {
                HashMap<String, Object> res = new HashMap<>();
                while (true) {
                    String key = "";
                    while (current != '<')
                        current = (char) fis.read();
                    current = (char) fis.read();
                    if (current == '/')
                        break;
                    while (current != '>') {
                        key += current;
                        current = (char) fis.read();
                    }
                    res.put(key, getValue(fis));
                    skipLine(fis);
                }
                return res;
            }
        } catch (Exception e) {
            System.out.println("Error: " + e);
        }
        return null;
    }

    public static void skipLine(FileInputStream fis) {
        char temp = ' ';
        try {
            while (temp != '\n')
                temp = (char) fis.read();
        } catch (Exception e) {
            System.out.println("Error: " + e);
        }
    }

    public static void main(String[] args) {
        File file = new File("filename.txt");
        try {
            FileInputStream fis = new FileInputStream(file);
            char current;
            HashMap<String, Object> hm = new HashMap<>();
            skipLine(fis);
            skipLine(fis);
            while (fis.available() > 0) {
                current = (char) fis.read();
                String key = "";
                if (current == '<') {
                    current = (char) fis.read();
                    if (current != '/') {
                        while (current != '>') {
                            key += current;
                            current = (char) fis.read();
                        }
                        hm.put(key, getValue(fis));
                    }
                }
            }
            for (Map.Entry m : hm.entrySet()) {
                System.out.println("Key: " + m.getKey() + " Value: " + m.getValue());
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
