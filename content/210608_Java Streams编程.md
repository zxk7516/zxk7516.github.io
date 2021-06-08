+++
title = "Java Stream 编程"
date = "2021-06-08"

[taxnonmies]
categories = ["java", "FP"]
+++


```java

import java.io.BufferedReader;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.Arrays;
import java.util.List;

public class Stream {

    public static void main(String[] args) {
        String filename = "C:\\Users\\o\\downloads\\The_Odyssey_-_Homer.txt";
        try (BufferedReader in = new BufferedReader(new FileReader(filename))) {
            Long long_words_counts = in.lines()
                    .parallel()
                    .map(
                            (String s) -> {
                                return (Long) Arrays.stream(s.split("\\PL+"))
                                        .filter(
                                                w -> w.length() > 12
                                        ).count();
                            }
                    ).reduce(
                            (Long) 0l,
                            (s, i) -> s + i
                    );
            System.out.println("long words count: " + long_words_counts);
        } catch (IOException e) {
            e.printStackTrace();
        }


    }
}

```