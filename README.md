# System_design-_URL_Shortener

import java.util.*;

class Codec {
    private final Map<String, String> map = new HashMap<>();
    private final Map<String, String> reverse = new HashMap<>();
    private final String base = "http://short.ly/";
    private int id = 1;
    public String encode(String longUrl) {
        if (reverse.containsKey(longUrl)) {
            return base + reverse.get(longUrl);
        }
        String code = Integer.toString(id++, 36);
        map.put(code, longUrl);
        reverse.put(longUrl, code);
        return base + code;
    }
    public String decode(String shortUrl) {
        String code = shortUrl.replace(base, "");
        return map.getOrDefault(code, "");
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Codec codec = new Codec();
        System.out.print("Enter a long URL: ");
        String longUrl = scanner.nextLine();
        String shortUrl = codec.encode(longUrl);
        System.out.println("Shortened URL: " + shortUrl);
    }
}
