

# Sorting a HashMap according to values in java

**Step1:** First to get all values of map considering that HashMap has unique values only.

**Step2:** Now put all the values in a list and sort this list with the **comparator** or **comparable interface** of Java.

**Step3:** Using step2 we will get sorted list of unique values. Now by iterating the list and traversing map again we compare
           entry.getValue from map with list element. if it is equal  get corresponding keys from the map and put it into 
           sortedmap which will eventually maintain the order. 

**Step4:** After insertion we would traverse same tree map which is sorted and is our resultant sorted map.

## CodeSnippet

```java
package com.bsmlabs.practice;

import java.util.*;

/***
 * Sort Hashmap by value
 * @author Mahendra
 * @return sorted hashmap
 */

public class HashMapSortByValue {
    public static void main(String[] args) {

        HashMap<String, String> hashMap = new HashMap<>();
        LinkedHashMap<String, String> sortedMap = new LinkedHashMap<>();
        List<String> list = new ArrayList<>();

        hashMap.put("14", "PuneethSai");
        hashMap.put("27", "Mahendra");
        hashMap.put("17", "Likitha");
        hashMap.put("1", "Swarna");
        hashMap.put("12", "Sravan");
        hashMap.put("24", "Winni");
        hashMap.put("08","Bunty");

        /**
         *  Step1: Add HashMap values into the list
         */

        for(Map.Entry<String, String> entry: hashMap.entrySet()) {
            list.add(entry.getValue());
        }

        /**
         * Step2: Approach1: Sort list elements using comparable or comparator interface in java
         * @return sorted list of elements
         */
         Collections.sort(list, new Comparator<String>() {
             @Override
             public int compare(String str1, String str2) {
                 return (str1).compareTo(str2);
             }
         });
         
         /**
         * Step2: Approach2: Using Lambda Expressions from Java8
         *  (str1, str2)-> (str1).compareTo(str2)
         */
        Collections.sort(list, (str1, str2) -> (str1).compareTo(str2));

        /**
         *  Step2: Approach3: Using Lambda Expressions with Method Reference.
         *  String::compareTo
         */
        Collections.sort(list, String::compareTo); //Lambda can be replaced with method reference.


        /**
         *  Step3: Iterate both list and hashMap get the sorted value from the list 
         *  and corresponding key by comparing value from list with hashMap value using
         *  entry.getValue() and put it in sortedMap which will maintain the order.
         *  
         */

        for(String str : list) {
             for(Map.Entry<String, String> entry: hashMap.entrySet()) {
                 if(entry.getValue().equals(str)){
                     sortedMap.put(entry.getKey(), str);
                 }
             }
         }

        System.out.println("Final SortedHashMap..."+sortedMap);



    }
}

```
**Output Result**
```
Final SortedHashMap... {08=Bunty, 17=Likitha, 27=Mahendra, 14=PuneethSai, 12=Sravan, 1=Swarna, 24=Winni}
```
