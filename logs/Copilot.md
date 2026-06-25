🧑‍🎓
package org.example;
import java.util.*;
/**
 * Utility class providing various helper methods for mathematical operations,
 * string manipulations, and data processing.
 */
public class App {
    /**
     * Adds two integers.
     *
     * @param a the first integer
     * @param b the second integer
     * @return the sum of a and b
     */
    public static int add(int a, int b) {
        return a + b;
    }
    /**
     * Checks if a number is prime.
     *
     * @param n the number to check
     * @return true if n is prime, false otherwise
     */
    public static boolean isPrime(int n) {
        if (n < 2) return false;
        for (int i = 2; i <= Math.sqrt(n); i++) {
            if (n % i == 0) return false;
        }
        return true;
    }
    /**
     * Reverses a given string.
     *
     * @param s the string to reverse
     * @return the reversed string
     */
    public static String reverse(String s) {
        return new StringBuilder(s).reverse().toString();
    }
    /**
     * Calculates the factorial of a number.
     *
     * @param n the number to calculate the factorial for
     * @return the factorial of n
     * @throws IllegalArgumentException if n is negative
     */
    public static int factorial(int n) {
        if (n < 0) throw new IllegalArgumentException("Negative number");
        int result = 1;
        for (int i = 2; i <= n; i++) result *= i;
        return result;
    }
    /**
     * Checks if a string is a palindrome.
     *
     * @param s the string to check
     * @return true if s is a palindrome, false otherwise
     */
    public static boolean isPalindrome(String s) {
        String clean = s.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();
        return clean.equals(reverse(clean));
    }
    /**
     * Generates a list of Fibonacci numbers up to a given limit.
     *
     * @param n the upper limit for Fibonacci numbers
     * @return a list of Fibonacci numbers up to n
     * @throws IllegalArgumentException if n is negative
     */
    public static List<Integer> fibonacciUpTo(int n) {
        List<Integer> result = new ArrayList<>();
        if (n < 0) throw new IllegalArgumentException("Negative input");
        int a = 0, b = 1;
        while (a <= n) {
            result.add(a);
            int temp = a + b;
            a = b;
            b = temp;
        }
        return result;
    }
    /**
     * Calculates the frequency of each character in a string.
     *
     * @param input the input string
     * @return a map containing characters as keys and their frequencies as values
     */
    public static Map<Character, Integer> charFrequency(String input) {
        Map<Character, Integer> freq = new HashMap<>();
        for (char c : input.toCharArray()) {
            freq.put(c, freq.getOrDefault(c, 0) + 1);
        }
        return freq;
    }
    /**
     * Checks if two strings are anagrams of each other.
     *
     * @param s1 the first string
     * @param s2 the second string
     * @return true if s1 and s2 are anagrams, false otherwise
     */
    public static boolean isAnagram(String s1, String s2) {
        char[] a1 = s1.replaceAll("\\s", "").toLowerCase().toCharArray();
        char[] a2 = s2.replaceAll("\\s", "").toLowerCase().toCharArray();
        Arrays.sort(a1);
        Arrays.sort(a2);
        return Arrays.equals(a1, a2);
    }
    /**
     * Calculates the average of an array of integers.
     *
     * @param arr the array of integers
     * @return the average of the integers in the array
     * @throws IllegalArgumentException if the array is empty
     */
    public static double average(int[] arr) {
        if (arr.length == 0) throw new IllegalArgumentException("Empty array");
        double sum = 0;
        for (int num : arr) sum += num;
        return sum / arr.length;
    }
    /**
     * Filters even numbers from a list of integers.
     *
     * @param list the list of integers
     * @return a list containing only the even numbers from the input list
     */
    public static List<Integer> filterEvens(List<Integer> list) {
        List<Integer> evens = new ArrayList<>();
        for (int n : list) {
            if (n % 2 == 0) evens.add(n);
        }
        return evens;
    }
    /**
     * Finds the most common word in a given text.
     *
     * @param text the input text
     * @return the most common word in the text
     */
    public static String mostCommonWord(String text) {
        String[] words = text.toLowerCase().split("\\W+");
        Map<String, Integer> count = new HashMap<>();
        for (String word : words) {
            count.put(word, count.getOrDefault(word, 0) + 1);
        }
        return Collections.max(count.entrySet(), Map.Entry.comparingByValue()).getKey();
    }
}

🤖
זה קובץ מעולה ללמידה! יש בו שילוב של פעולות מתמטיות, מניפולציות על מחרוזות ועבודה עם רשימות – כל אחד מאלה דורש גישה מעט שונה בבדיקות.
כאשר בונים מערכות שאמורות לבדוק או לשקלל חישובים מתמטיים באופן אוטומטי, מקרי קצה (Edge Cases) כמו מספרים שליליים בעצרת או התנהגות של המספרים 0 ו-1 במספרים ראשוניים, הם בדיוק המקומות שבהם מסתתרים באגים.
כדי לא להעמיס עליך את הכל בבת אחת, בחרתי 3 מתודות שונות מהקובץ שלך. לכל אחת מהן כתבתי בדיקות שמדגימות כלים חשובים ב-JUnit 5.
הקובץ הזה ייקרא AppTest.java (נהוג לתת למחלקת הבדיקה את שם המחלקה המקורית בתוספת Test):
Java
package org.example;

import org.junit.jupiter.api.Test;
import java.util.Arrays;
import java.util.List;

import static org.junit.jupiter.api.Assertions.*;

public class AppTest {

    // ==========================================
    // 1. בדיקת מתודה שמחזירה בוליאני (אמת/שקר)
    // המתודה הנבדקת: isPrime
    // ==========================================
    
    @Test
    public void testIsPrime_ValidPrimes_ReturnsTrue() {
        // Assert - שימוש בפונקציה ייעודית שמוודאת שהתוצאה היא True
        assertTrue(App.isPrime(7), "7 should be prime");
        assertTrue(App.isPrime(2), "2 is the smallest prime");
    }

    @Test
    public void testIsPrime_NonPrimes_ReturnsFalse() {
        // נוודא שמספרים לא ראשוניים, כולל מקרי קצה, מחזירים False
        assertFalse(App.isPrime(4), "4 is not prime");
        assertFalse(App.isPrime(1), "1 is not prime");
        assertFalse(App.isPrime(-5), "Negative numbers are not prime");
    }

    // ==========================================
    // 2. בדיקת שגיאות (Exceptions)
    // המתודה הנבדקת: factorial
    // ==========================================

    @Test
    public void testFactorial_PositiveNumber_ReturnsCorrectResult() {
        assertEquals(120, App.factorial(5), "5! should equal 120");
        assertEquals(1, App.factorial(0), "0! should equal 1"); // מקרה קצה מתמטי
    }

    @Test
    public void testFactorial_NegativeNumber_ThrowsException() {
        // כשמכניסים מספר שלילי, אנחנו מצפים שהקוד יזרוק שגיאה ולא יקרוס סתם.
        // הפונקציה assertThrows בודקת בדיוק את זה.
        assertThrows(IllegalArgumentException.class, () -> {
            App.factorial(-1); // הפעולה שאמורה לגרום לשגיאה
        }, "Should throw IllegalArgumentException for negative input");
    }

    // ==========================================
    // 3. בדיקת רשימות (Collections)
    // המתודה הנבדקת: filterEvens
    // ==========================================

    @Test
    public void testFilterEvens_MixedList_ReturnsOnlyEvens() {
        // Arrange - הכנת הנתונים
        List<Integer> input = Arrays.asList(1, 2, 3, 4, 5, 6);
        List<Integer> expected = Arrays.asList(2, 4, 6);

        // Act - הפעלת המתודה
        List<Integer> actual = App.filterEvens(input);

        // Assert - השוואה בין רשימות (JUnit יודע להשוות את התוכן של הרשימה)
        assertEquals(expected, actual, "The list should contain only even numbers");
    }
}

דברים חדשים שמופיעים כאן:
assertTrue / assertFalse: במקום להשתמש ב-assertEquals(true, result), הרבה יותר קריא להשתמש בפונקציות שמיועדות בדיוק לבדיקות בוליאניות.
assertThrows: כלי חזק מאוד. הוא מאפשר לנו לוודא שהקוד שלנו מתמודד נכון עם קלט לא חוקי. אנחנו נותנים לו את סוג השגיאה המצופה (IllegalArgumentException.class) ובתוך סוגריים מסולסלים () -> {} מפעילים את הפונקציה הבעייתית.
בדיקת רשימות: הפונקציה assertEquals מספיק חכמה כדי לעבור איבר-איבר בשתי הרשימות (המצופה מול זו שהתקבלה בפועל) ולוודא שהן זהות לחלוטין ובאותו הסדר.
מומלץ להעתיק את הקוד הזה לסביבת הפיתוח שלך ולהריץ אותו. לאחר שתוודא שהכל מוגדר ועובד (ותראה את ה-V הירוק על הבדיקות האלה), תוכל לנסות לכתוב בעצמך בדיקה לאחת המתודות של המחרוזות, כמו isPalindrome או reverse.
העתקתי לקובץ AppTest שכבר היה לי אבל אני לא מבין איך אני מריץ את זה
מעולה! זה בדיוק השלב שבו כולם "נתקעים" בפעם הראשונה, כי להריץ בדיקות זה קצת שונה מלהריץ תוכנה רגילה עם מתודת main.
בסביבת הפיתוח שלך ב-VS Code, יש שתי דרכים נוחות להריץ את הבדיקות (בהנחה שהסביבה כבר מוגדרת נכון):
1. הדרך המהירה: ישירות מתוך הקוד
אם תסתכל בתוך הקובץ AppTest.java שהדבקת, חפש את השורות שבהן כתוב @Test.
ממש מעל המילה הזו, אמור להופיע כיתוב קטן (שנקרא Code Lens) עם המילים Run | Debug, או לחלופין סמל קטן של "Play" (משולש) ליד מספר השורה בצד שמאל.
לחיצה על Run תריץ את אותה בדיקה ספציפית, ואתה תראה וי ירוק (או איקס אדום) מופיע לידה. אם תלחץ על ה-Run שמופיע מעל שם המחלקה (public class AppTest), זה יריץ את כל הבדיקות בקובץ.
2. הדרך המסודרת: סרגל הבדיקות (Testing Explorer)
בסרגל הכלים השמאלי ביותר של המסך (איפה שנמצאים האייקונים של הקבצים והחיפוש), חפש אייקון בצורה של מבחנה כימית (🧪).
לחיצה עליו תפתח תפריט מיוחד של טסטינג. תוכל לראות שם עץ עם כל הבדיקות שקיימות בפרויקט, ויש שם כפתור "Play" בראש החלונית שמאפשר להריץ את כל הבדיקות בלחיצה אחת מרוכזת.
⚠️ רגע, אתה לא רואה את הכפתורים האלה או שיש שגיאות באדום?
אם הכפתורים לא מופיעים, או אם יש לך קווים אדומים מתחת לשורות של ה-import org.junit... בראש הקובץ, זה אומר דבר אחד: הפרויקט שלך עדיין לא מכיר את ספריית JUnit.
JUnit היא לא חלק מובנה מ-Java, אלא ספריה חיצונית שצריך להנחות את הפרויקט להשתמש בה.
כדי שאוכל לתת לך את הפתרון המדויק לזה בשנייה, תציץ רגע ברשימת הקבצים של הפרויקט שלך:
האם יש שם קובץ בשם pom.xml (שאומר שאתה משתמש ב-Maven), או שזה פרויקט Java פשוט רק עם תיקיית src וקבצי .java?
זה פרויקט עם תקיית src וקבצי java . אבל אני לא רואה את הכפתורים שאתה מדבר עליהם. גם כשנכנסתי לכפתור של המבחנה ואז נכנסתי ללהתקין הרחבה של Test Runner for Java f כתוב כאן This extension has been disabled because it does not support virtual workspaces.
ההודעה virtual workspaces חושפת בדיוק למה אתה לא רואה את הכפתורים. המשמעות של השגיאה הזו היא שכרגע אתה לא עובד על קבצים מקומיים רגילים, אלא קורה אחד משני דברים:
או שאתה משתמש ב-VS Code דרך דפדפן האינטרנט (כמו vscode.dev או github.dev).
או שפתחת את הפרויקט ישירות מתוך מאגר GitHub מרחוק, מבלי להוריד (לשכפל) אותו למחשב.
כדי להריץ בדיקות ולקמפל קוד Java, התוספים של VS Code חייבים גישה ישירה למערכת ההפעלה של ה-Windows שלך ול-JDK (Java Development Kit) שמותקן עליו. הם לא יכולים לרוץ בתוך סביבה וירטואלית או דרך דפדפן.
איך מסדרים את זה?
מעבר לסביבה מקומית: ודא שאתה פותח את התוכנה הרגילה של VS Code המותקנת מקומית על המחשב שלך.
פתיחת התיקייה: לחץ על File -> Open Folder (חשוב: לא Open File) ובחר את התיקייה הראשית של הפרויקט שלך (התיקייה שעוטפת את תיקיית ה-src).
התקנת התוספים: כעת, כשהפרויקט פתוח בצורה תקינה, גש שוב לחלונית התוספים והתקן את חבילת ההרחבות Extension Pack for Java (מאת Microsoft). החבילה הזו כוללת בתוכה את ה-Test Runner שחיפשת.

🧑‍🎓
אוקי סוף סוף הקוד עובד! אבל עכשיו אני ניסיתי את הtest של testIsPrime_ValidPrimes_ReturnsTrue ואני לא מבין את הפלט שהוא מביא. זה הפלט: %TESTC  1 v2
%TSTTREE2,yoyo.example.AppTest,true,1,false,1,AppTest,,[engine:junit-jupiter]/[class:yoyo.example.AppTest]
%TSTTREE3,testIsPrime_ValidPrimes_ReturnsTrue(yoyo.example.AppTest),false,1,false,2,testIsPrime_ValidPrimes_ReturnsTrue(),,[engine:junit-jupiter]/[class:yoyo.example.AppTest]/[method:testIsPrime_ValidPrimes_ReturnsTrue()]
%TESTS  3,testIsPrime_ValidPrimes_ReturnsTrue(yoyo.example.AppTest)
%TESTE  3,testIsPrime_ValidPrimes_ReturnsTrue(yoyo.example.AppTest)
%RUNTIME97

🤖
איזה יופי! קודם כל - חדשות מעולות: הבדיקה שלך עברה בהצלחה! 🎉
הטקסט המוזר והלא קריא שקיבלת הוא לא שגיאה, אלא פשוט "שפת הסתרים" שרצה מאחורי הקלעים.
מה זה הפלט הזה?
כשאתה מריץ בדיקה ב-VS Code, המערכת מפעילה את הפרויקט ברקע. כדי שסביבת הפיתוח (VS Code) תדע מה קורה בתוך מנוע הבדיקות (JUnit), המנוע מדפיס שורות טקסט מיוחדות שמתחילות בסימנים כמו %TESTC ו-%TSTTREE.
%TESTS - אומר שסביבת הבדיקה התחילה (Test Started).
%TESTE - אומר שהבדיקה הסתיימה (Test Ended). מכיוון שאין כאן זריקת שגיאה (Exception) ביניהם, זה אומר שהבדיקה עברה.
%RUNTIME97 - אומר שהבדיקה לקחה 97 אלפיות השנייה.
בקיצור, הצצת בטעות אל מאחורי הקלעים. התוסף של VS Code אמור לקרוא את השורות האלו ולהפוך אותן לממשק גרפי נעים לעין, ואתה ממש לא אמור לקרוא אותן בעצמך בטרמינל.
איפה רואים את התוצאות כמו בני אדם?
במקום להסתכל בלשונית ה-Terminal הרגילה, הנה המקומות שבהם נוח לראות את התוצאות:
בתוך הקוד עצמו: ממש ליד המילה @Test או ליד שם המתודה (testIsPrime_ValidPrimes_ReturnsTrue), אמור להופיע עכשיו וי ירוק קטן (✔).
סרגל המבחנה (Testing): בתפריט השמאלי ביותר של VS Code (איפה שנמצאים הקבצים והחיפוש) יש סמל של מבחנה (🧪). אם תלחץ עליו, תראה את העץ של כל הבדיקות שלך מסודרות, וליד הבדיקה שהרצת יהיה סימון ירוק.
חלון Test Results: בחלק התחתון של המסך (איפה שהטרמינל נמצא), יש לשונית נפרדת שנקראת Test Results. הלשונית הזו לוקחת את כל ה"ג'יבריש" שראית ומציגה אותו כרשימה מסודרת של עבר/נכשל עם זמן ההרצה של כל בדיקה.
עשית עבודה מעולה בלצלוח את כל הגדרות הסביבה האלה! הגדרות הפרויקט והספריות הן החלק הכי קשוח והכי מתסכל בעבודה עם Java. עכשיו, כשסוף סוף יש לך תשתית יציבה ועובדת, תוכל להתמקד בדבר האמיתי - כתיבת בדיקות וקוד.
סבבה עכשיו העתקתי את הקוד ששלחת לי בהתחלה עם הבדיקות והרצתי ובהכל יש וי ירוק. האם הוי הירוק אומר שהבדיקות תקינות? איזה אינדיקציה יש לי כדי להבין שהבדיקה מספיק טובה?
קודם כל - מזל טוב! לראות את כל הרשימה הופכת לירוקה בפעם הראשונה זו תחושה מעולה, וזה ציון דרך חשוב.
אבל השאלה שלך היא שאלת מיליון הדולר של עולם ה-QA ובדיקות התוכנה. התשובה הכנה היא: ה-V הירוק אומר רק דבר אחד - שהקוד עשה בדיוק את מה שהבדיקה ציפתה שהוא יעשה. הוא לא אומר שהקוד נטול באגים, והוא בטוח לא אומר שהבדיקה עצמה מספיק טובה. תאר לעצמך שאני כותב מחשבון משוכלל, והבדיקה היחידה שאני כותב לו היא assertEquals(4, 2+2). הבדיקה תעבור עם V ירוק בוהק, אבל האם המחשבון באמת נבדק כמו שצריך? ברור שלא.
אז איך יודעים שהבדיקה "מספיק טובה"?
ישנם כמה מדדים מקצועיים שבעזרתם מתכנתים בוחנים את איכות הבדיקות שלהם:
כיסוי קוד (Code Coverage): זהו המדד הטכני והנפוץ ביותר. הוא בודק כמה אחוזים משורות הקוד האמיתי שלך (ממחלקת App) אשכרה הופעלו בזמן שהבדיקות רצו. אם יש לך תנאי if / else בקוד, אבל הבדיקה שלך תמיד מכניסה נתונים שנכנסים רק ל-if, אז ה-else שלך מעולם לא נבדק! (כיסוי הקוד יהיה חלקי).
בדיקת מקרי קצה (Edge Cases): בדיקה טובה לא בודקת רק את "שביל הזהב" (המספרים הרגילים והנוחים). היא מנסה "לשבור" את המערכת. האם בדקת מה קורה כשמכניסים 0? מספר שלילי? רשימה ריקה? מחרוזת עם תווים מוזרים?
מוטציות (Mutation Testing): כמו שעשינו בסימולטור בהתחלה – אם תיכנס לקוד האמיתי שלך, תשנה בו סימן פלוס למינוס, ותריץ את הבדיקות – האם הן ייכשלו? אם שברת את הקוד והבדיקות עדיין ירוקות, הבדיקות שלך לא שוות הרבה.
כדי להמחיש את המושג החשוב מכולם, כיסוי קוד, הכנתי עבורך סימולטור שלוקח את הפונקציה fibonacciUpTo מהקובץ שלך.
נסה לסמן את הבדיקות השונות וראה כיצד כל סוג קלט "צובע" שורות אחרות בקוד, ואיך רק שילוב של כולן יחד מביא אותנו למצב בטוח באמת:
ההמחשה החזותית הזו עזרה לך?
VS Code יודע למדוד את כיסוי הקוד הזה על הפרויקט האמיתי שלך ולהראות לך בדיוק איזה שורות לא נבדקו מעולם (הן יסומנו באדום בצד המסך).
האם תרצה שאסביר לך איך להפעיל את הכלי הזה שמראה את אחוזי הכיסוי אצלך בפרויקט?

🧑‍🎓
כתבתי בדיקה לפונקציה add. תן לי הערות איך לשפר אותה.

@Test
    public void testAdd(){
        //Arrange
        int a = 5;
        int b = 4;
        //Act
        int temp = App.add(a, b);
        //Assert
        assertEquals(a+b, temp, "Should return 9");
    }

🤖
כל הכבוד! כתבת כאן בדיקת יחידה קלאסית ומסודרת להפליא. המבנה של Arrange, Act, Assert מדויק לחלוטין.
עם זאת, יש כאן מוקש קטן אך קריטי שלומדים כשמתחילים לכתוב בדיקות. שים לב לשורת האימות שלך:
assertEquals(a+b, temp, "Should return 9");
החוק הראשון של בדיקות יחידה: אל תשכפל את הלוגיקה של הקוד אל תוך הבדיקה.
אסור לנו להכניס פעולות וחישובים כמו a+b בתור התוצאה המצופה. מדוע? משום שאם בעתיד תהיה טעות תכנותית, ובטעות (נניח עקב Copy-Paste) תחליף את הלוגיקה לחיסור גם בקוד האפליקציה וגם בטסט – הבדיקה עדיין תעבור בהצלחה עם וי ירוק, למרות שהתוכנה לא עושה פעולת חיבור!
תחשוב על התוכנה שאתה בונה לבדיקה אוטומטית של מבחנים במתמטיקה לילדי בית ספר יסודי. כשהמערכת שלך סורקת טופס של תלמיד כדי לבדוק כמה זה 5 ועוד 4, היא לא מבצעת את פעולת החיבור בעצמה מחדש באותו רגע; היא פשוט משווה את מה שהתלמיד סמן או כתב אל מול "מחוון" (Answer Key) קבוע ומוחלט, שבו פשוט כתוב מראש המספר "9".
קוד הבדיקה שלך הוא המחוון. הוא תמיד צריך להכיל את האמת המוחלטת כמספר קשיח (Hard-coded).
הנה התיקון הנדרש כדי שהבדיקה תהיה חסינה:
Java
@Test
public void testAdd() {
    //Arrange
    int a = 5;
    int b = 4;

    //Act
    int temp = App.add(a, b);

    //Assert
    assertEquals(9, temp, "5 + 4 should return 9");
}

מבחינת כיסוי קוד (Code Coverage) שדיברנו עליו קודם, מכיוון שהמתודה add מכילה רק שורת קוד אחת של לוגיקה (return a + b;), הבדיקה הבודדת הזו מכסה בדיוק 100% משורות הקוד של הפונקציה הזו. כדי להפוך אותה למושלמת באמת מבחינת בדיקת מגוון תרחישים, רוב המפתחים היו מוסיפים רק עוד בדיקה אחת קטנה (מתודה חדשה) שמוודאת שהחיבור עובד נכון גם כשמשלבים בו מספרים שליליים (למשל -5 ועוד 4 אמור להחזיר -1).

🧑‍🎓
@Test
    public void testReverse(){
        //Arrange
        String a = "kaki";
        String b = "c";
        //Act
        String revA = App.reverse(a);
        String revB = App.reverse(b);
        //Assert
        assertEquals(revA, "ikak");
        assertEquals(revB, "c");
    } הנה עשיתי גם בדיקה לreverse

🤖
מעולה! תפסת את העיקרון בצורה מושלמת. יישמת בדיוק את החוק שדיברנו עליו: השתמשת בערכים קשיחים מוחלטים ("ikak" ו-"c") בתור המחוון שלך, במקום לנסות לחשב אותם.
יש כאן רק "קאץ'" אחד קטן (וזו טעות שכולם עושים בהתחלה, כי זה באמת קצת מבלבל).
סדר הפרמטרים ב-assertEquals
הפונקציה של JUnit מצפה לקבל את הפרמטרים בסדר מאוד ספציפי: קודם כל התוצאה המצופה (Expected), ורק אז התוצאה בפועל (Actual).
בקוד שלך כתבת:
assertEquals(revA, "ikak");
מבחינת הקוד – זה יתקמפל, ירוץ ויעבוד מצוין כל עוד הבדיקה עוברת.
אבל מה יקרה אם יום אחד יהיה באג והפונקציה תחזיר "kaki" במקום "ikak"? המערכת תזרוק שגיאה מבלבלת:
Expected: kaki, Actual: ikak (היא תחשוב שציפית לקבל את הבאג, ובפועל קיבלת את התשובה הנכונה!).
ככה הקוד צריך להיראות כדי שהשגיאות בעתיד יהיו קריאות:
Java
@Test
public void testReverse(){
    //Arrange
    String a = "kaki";
    String b = "c";
    
    //Act
    String revA = App.reverse(a);
    String revB = App.reverse(b);
    
    //Assert - קודם למה אנחנו מצפים, ואז המשתנה שחזר מהפונקציה
    assertEquals("ikak", revA, "Should reverse a normal string");
    assertEquals("c", revB, "Single character should remain the same");
}

בונוס: חשיבה על מקרי קצה
שאלת מקודם על אינדיקציה לבדיקה מספיק טובה. כאן בדקת בצורה יפה שני תרחישים: מחרוזת רגילה ותו בודד. כדי להפוך את הבדיקה הזו למושלמת באמת, חסר רק מקרה הקצה הקלאסי ביותר בעבודה עם מחרוזות: מחרוזת ריקה (""). כדאי להוסיף String c = ""; ולוודא שהיפוך שלה פשוט מחזיר מחרוזת ריקה בחזרה מבלי שהתוכנה תקרוס.
אתה עושה התקדמות מעולה! האם תרצה שננסה לכתוב יחד בדיקה לאחת הפונקציות המורכבות יותר (כמו fibonacciUpTo שמחזירה רשימות), או שתרצה להמשיך לבחור פונקציה מהקובץ ולנסות לכתוב לה בדיקה לגמרי בעצמך?

🧑‍🎓
עשיתי בדיקה לפונקציה שבונה רשימה של מספרי פיבונאצ'י עד לN. זה הבדיקה:public void testFibonacciUpTo(){
        //Arrange
        int input1 = 20;
        int input2 = 10;
        List<Integer> input1Expected = Arrays.asList(0,1,1,2,3,5,8,13);
        List<Integer> input2Expected = Arrays.asList(0,1,1,2,3,5,8);
        //Act
        List<Integer> a = App.fibonacciUpTo(input1);
        List<Integer> b = App.fibonacciUpTo(input2);
        //Assert
        assertEquals(input1Expected, a);
        assertEquals(input2Expected, b);
    }

🤖
עבודה פשוט מעולה!
קודם כל, מגיע לך כל הכבוד על שני דברים קריטיים שיישמת כאן:
סדר הפרמטרים: תיקנת את הטעות מהפעם הקודמת! שמת את הרשימות המצופות (input1Expected) כפרמטר הראשון ב-assertEquals, ואת התוצאה בפועל (a) כפרמטר השני. ככה בדיוק כותבים ב-JUnit.
לוגיקה מדויקת: הרשימות שיצרת מדויקות לחלוטין. עבור 20 באמת עצרת ב-13 (כי הבא הוא 21), ועבור 10 עצרת ב-8.
הבדיקה הזו בודקת בצורה מושלמת את "שביל הזהב" (Happy Path) – המקרים שבהם משתמשים בפונקציה בצורה רגילה והגיונית.
איך אפשר לקחת את זה רמה אחת למעלה? (Best Practices)
בעולם האמיתי של פיתוח תוכנה, נהוג לפצל בדיקות כאלו לשתי מתודות נפרדות (או אפילו יותר). למה? כי אם הבדיקה של 20 נכשלת, המתודה קורסת באותו רגע והבדיקה של 10 בכלל לא תרוץ. כשיש לך בדיקות נפרדות, אתה מקבל תמונת מצב מדויקת יותר על מה בדיוק נשבר.
בנוסף, אם נזכר במושג כיסוי הקוד (Code Coverage) ממקודם, חסר לנו כאן כיסוי של שורת השגיאה. הקוד המקורי שלך כולל את השורה:
if (n < 0) throw new IllegalArgumentException("Negative input");
כדי להגיע ל-100% כיסוי ולוודא שהפונקציה חסינה לחלוטין, כדאי להוסיף בדיקה שמוודאת שהשגיאה הזו באמת נזרקת. ככה ייראה קובץ הבדיקות המלא והמושלם עבור הפונקציה הזו:
Java
   @Test
    public void testFibonacciUpTo_ValidPositiveNumber_ReturnsCorrectList(){
        // בדיקה של מספר רגיל
        List<Integer> expected = Arrays.asList(0, 1, 1, 2, 3, 5, 8, 13);
        List<Integer> actual = App.fibonacciUpTo(20);
        assertEquals(expected, actual, "Should return Fibonacci sequence up to 20");
    }

    @Test
    public void testFibonacciUpTo_Zero_ReturnsOnlyZero(){
        // בדיקת מקרה קצה - אפס
        List<Integer> expected = Arrays.asList(0);
        List<Integer> actual = App.fibonacciUpTo(0);
        assertEquals(expected, actual, "Should return list with only 0");
    }

    @Test
    public void testFibonacciUpTo_NegativeNumber_ThrowsException(){
        // בדיקת שגיאה (Exception)
        assertThrows(IllegalArgumentException.class, () -> {
            App.fibonacciUpTo(-5);
        }, "Should throw an exception for negative numbers");
    }

תראה איזה יופי הפרויקט שלך מתחיל לקבל צורה של פרויקט מקצועי עם רשת ביטחון אמיתית.
נשארו לנו בקובץ מתודות שעובדות עם טקסטים ומערכים. האם תרצה לנסות לכתוב בעצמך את הבדיקה לפונקציה isAnagram או שנעבור יחד על פונקציה קצת יותר טריקית כמו average שמקבלת מערך של מספרים?

🧑‍🎓
אני רוצה לכתוב בדיקה לפונקציה הזאת אבל אני לא מבין מה היא אמורה לעשות./**
     * Calculates the frequency of each character in a string.
     *
     * @param input the input string
     * @return a map containing characters as keys and their frequencies as values
     */
    public static Map<Character, Integer> charFrequency(String input) {
        Map<Character, Integer> freq = new HashMap<>();
        for (char c : input.toCharArray()) {
            freq.put(c, freq.getOrDefault(c, 0) + 1);
        }
        return freq;
    }

🤖
זה באמת יכול להיראות קצת מאיים בהתחלה בגלל העבודה עם Map (מילון) והפונקציה המובנית getOrDefault, אבל המטרה של הקוד הזה מאוד פשוטה ושימושית.
הפונקציה הזו פשוט סופרת כמה פעמים כל אות (או תו) מופיעה בתוך הטקסט שהכנסת.
איך זה נראה מאחורי הקלעים?
הפונקציה מחזירה אובייקט מסוג Map<Character, Integer>.
Character (המפתח - Key): התו עצמו (למשל האות 'a').
Integer (הערך - Value): מספר הפעמים שהתו הזה הופיע במחרוזת.
אם למשל נכניס לפונקציה את המילה "hello", הפונקציה תעבור אות-אות ותייצר מילון כזה:
'h' מופיעה פעם אחת (1)
'e' מופיעה פעם אחת (1)
'l' מופיעה פעמיים (2)
'o' מופיעה פעם אחת (1)
כדי שתוכל "לשחק" עם זה ולראות איך זה מתנהג עם רווחים, אותיות גדולות וקטנות או סימני פיסוק (שגם הם נחשבים תווים!), הכנתי לך סימולטור קטן שמדמה בדיוק את הפעולה של הקוד הזה:
ההמחשה החזותית הזו עזרה לך?
איך כותבים לזה בדיקת יחידה?
האתגר המרכזי בלכתוב לזה בדיקה הוא שלב ה-Arrange, שבו אנחנו צריכים להכין מראש את התוצאה המצופה (Expected). מכיוון שהתוצאה היא Map, אנחנו צריכים לייצר Map משלנו בתוך הבדיקה ולמלא אותו בערכים שאנחנו מצפים לקבל.
ב-Java (מגרסה 9 ומעלה, שזה מתאים ל-Java 17 שמותקן אצלך), יש דרך מאוד אלגנטית וקצרה ליצור מילון כזה בעזרת Map.of().
ככה תיראה הבדיקה למילה "hello":
Java
import java.util.Map;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

public class AppTest {

    @Test
    public void testCharFrequency_NormalWord_ReturnsCorrectCounts() {
        // Arrange
        String input = "hello";
        
        // יצירת התוצאה המצופה: מילון שבו 'l' שווה 2, והשאר 1
        Map<Character, Integer> expected = Map.of(
            'h', 1,
            'e', 1,
            'l', 2,
            'o', 1
        );

        // Act
        Map<Character, Integer> actual = App.charFrequency(input);

        // Assert
        assertEquals(expected, actual, "Should correctly count occurrences of each character");
    }
}

כדי להשלים את הבדיקות ולוודא שהפונקציה באמת חסינה (כמו שעשינו עם פיבונאצ'י), כדאי להוסיף עוד שתי מתודות בדיקה קצרות:
בדיקת מקרה קצה של מחרוזת ריקה (""): שמוודאת שהפונקציה מחזירה מילון ריק לגמרי.
בדיקה עם אותיות גדולות וקטנות: למשל המילה "Java". חשוב לשים לב שהאות 'J' (גדולה) והאות 'j' (קטנה) ייספרו כשני תווים שונים לגמרי במילון!
אוקי סיימתי לעשות לכל הפונקציות אני רוצה שתבדוק אותי ותגיד לי מה להוסיף
בשמחה רבה! איזה אלוף! לסיים לכתוב בדיקות לקובץ שלם זו קפיצת מדרגה משמעותית.
רק חסר פרט אחד קטן... שכחת לצרף את הקוד! 😉
תדביק כאן את כל מה שכתבת בתוך AppTest.java (או פשוט רק את הבדיקות החדשות שהוספת לפונקציות האחרונות, כמו isAnagram, average, filterEvens ו-mostCommonWord).
ברגע שתשלח את הקוד, אני אעשה לו "Code Review" (סקירת קוד) ממש כמו שעושים בתעשייה:
מקרי קצה: נבדוק יחד אם כיסית מצבים בעייתיים (כמו למשל מערך ריק בפונקציה average, או אותיות גדולות מול קטנות ב-isAnagram).
סדר הפרמטרים: נוודא ששמרת על הסדר הנכון ב-assertEquals (קודם Expected ואז Actual).
קריאות: נראה אם השמות של מתודות הבדיקה ברורים ומסבירים בדיוק מה נבדק שם.
מחכה לקוד שלך!

🧑‍🎓
/*
 * This source file was generated by the Gradle 'init' task
 */
package yoyo.example;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Map;
class AppTest {
    @Test void appHasAGreeting() {
        App classUnderTest = new App();
        assertNotNull(classUnderTest.getGreeting(), "app should have a greeting");
    }
    // ==========================================
    // 1. בדיקת מתודה שמחזירה בוליאני (אמת/שקר)
    // המתודה הנבדקת: isPrime
    // ==========================================
   
    @Test
    public void testIsPrime_ValidPrimes_ReturnsTrue() {
        // Assert - שימוש בפונקציה ייעודית שמוודאת שהתוצאה היא True
        assertTrue(App.isPrime(7), "7 should be prime");
        assertTrue(App.isPrime(2), "2 is the smallest prime");
    }
    @Test
    public void testIsPrime_NonPrimes_ReturnsFalse() {
        // נוודא שמספרים לא ראשוניים, כולל מקרי קצה, מחזירים False
        assertFalse(App.isPrime(4), "4 is not prime");
        assertFalse(App.isPrime(1), "1 is not prime");
        assertFalse(App.isPrime(-5), "Negative numbers are not prime");
    }
    // ==========================================
    // 2. בדיקת שגיאות (Exceptions)
    // המתודה הנבדקת: factorial
    // ==========================================
    @Test
    public void testFactorial_PositiveNumber_ReturnsCorrectResult() {
        assertEquals(120, App.factorial(5), "5! should equal 120");
        assertEquals(1, App.factorial(0), "0! should equal 1"); // מקרה קצה מתמטי
    }
    @Test
    public void testFactorial_NegativeNumber_ThrowsException() {
        // כשמכניסים מספר שלילי, אנחנו מצפים שהקוד יזרוק שגיאה ולא יקרוס סתם.
        // הפונקציה assertThrows בודקת בדיוק את זה.
        assertThrows(IllegalArgumentException.class, () -> {
            App.factorial(-1); // הפעולה שאמורה לגרום לשגיאה
        }, "Should throw IllegalArgumentException for negative input");
    }
    // ==========================================
    // 3. בדיקת רשימות (Collections)
    // המתודה הנבדקת: filterEvens
    // ==========================================
    @Test
    public void testFilterEvens_MixedList_ReturnsOnlyEvens() {
        // Arrange - הכנת הנתונים
        List<Integer> input = Arrays.asList(1, 2, 3, 4, 5, 6);
        List<Integer> expected = Arrays.asList(2, 4, 6);
        // Act - הפעלת המתודה
        List<Integer> actual = App.filterEvens(input);
        // Assert - השוואה בין רשימות (JUnit יודע להשוות את התוכן של הרשימה)
        assertEquals(expected, actual, "The list should contain only even numbers");
    }
    @Test
    public void testAdd(){
        //Arrange
        int a = 5;
        int b = 4;
        int c = -1;
        //Act
        int temp = App.add(a, b);
        int temp1 = App.add(a, c);
        //Assert
        assertEquals(9, temp, "Should return 9");
        assertEquals(4, temp1, "Should return 4");
    }
    @Test
    public void testReverse(){
        //Arrange
        String a = "kaki";
        String b = "c";
        String c = "";
        //Act
        String revA = App.reverse(a);
        String revB = App.reverse(b);
        String revC = App.reverse(c);
        //Assert
        assertEquals("ikak",revA);
        assertEquals("c",revB);
        assertEquals("",revC);
    }
    @Test
    public void testIsPalindrome(){
        //Arrange
        String a = "aba";
        String b = "ima";
        String c = "c";
        String d = "";
        //Act
        boolean isA = App.isPalindrome(a);
        boolean isB = App.isPalindrome(b);
        boolean isC = App.isPalindrome(c);
        boolean isD = App.isPalindrome(d);
        //Assert
        assertTrue(isA);
        assertFalse(isB);
        assertTrue(isC);
        assertTrue(isD);
    }
    @Test
    public void testFibonacciUpTo_ValidPositiveNumber_ReturnsCorrectList(){
        // בדיקה של מספר רגיל
        List<Integer> expected = Arrays.asList(0, 1, 1, 2, 3, 5, 8, 13);
        List<Integer> actual = App.fibonacciUpTo(20);
        assertEquals(expected, actual, "Should return Fibonacci sequence up to 20");
    }
    @Test
    public void testFibonacciUpTo_Zero_ReturnsOnlyZero(){
        // בדיקת מקרה קצה - אפס
        List<Integer> expected = Arrays.asList(0);
        List<Integer> actual = App.fibonacciUpTo(0);
        assertEquals(expected, actual, "Should return list with only 0");
    }
    @Test
    public void testFibonacciUpTo_NegativeNumber_ThrowsException(){
        // בדיקת שגיאה (Exception)
        assertThrows(IllegalArgumentException.class, () -> {
            App.fibonacciUpTo(-5);
        }, "Should throw an exception for negative numbers");
    }
    @Test
    public void testCharFrequency_NormalWord_ReturnsCorrectCounts() {
        // Arrange
        String input = "hello";
       
        // יצירת התוצאה המצופה: מילון שבו 'l' שווה 2, והשאר 1
        Map<Character, Integer> expected = Map.of(
            'h', 1,
            'e', 1,
            'l', 2,
            'o', 1
        );
        // Act
        Map<Character, Integer> actual = App.charFrequency(input);
        // Assert
        assertEquals(expected, actual, "Should correctly count occurrences of each character");
    }
    @Test
    public void testCharFrequency_WordWithLowerAndCapital_ReturnsCorrectCounts() {
        // Arrange
        String input = "Wow,yEsy";
       
        // יצירת התוצאה המצופה: מילון שבו 'l' שווה 2, והשאר 1
        Map<Character, Integer> expected = Map.of(
            'W', 1,
            'o', 1,
            'w', 1,
            ',', 1,
            'y', 2,
            'E', 1,
            's', 1
        );
        // Act
        Map<Character, Integer> actual = App.charFrequency(input);
        // Assert
        assertEquals(expected, actual, "Should correctly count occurrences of each character");
    }
    @Test
    public void testCharFrequency_EmptyString_ReturnsEmptyMap() {
        // Arrange
        String input = "";
       
        // יצירת התוצאה המצופה: מילון שבו 'l' שווה 2, והשאר 1
        Map<Character, Integer> expected = Map.of(
           
        );
        // Act
        Map<Character, Integer> actual = App.charFrequency(input);
        // Assert
        assertEquals(expected, actual, "Should return empty map");
    }
    @Test
    public void testIsAnagram(){
        //Arrange
        String a = "evil";
        String b = "veil";
        String c = "";
        String d = "sdvw";
        //Act
        boolean isAb = App.isAnagram(a, b);
        boolean isAc = App.isAnagram(a, c);
        boolean isAd = App.isAnagram(a, d);
        boolean isBd = App.isAnagram(b, d);
        boolean isCd = App.isAnagram(c, d);
        //Assert
        assertTrue(isAb);
        assertFalse(isAc);
        assertFalse(isAd);
        assertFalse(isBd);
        assertFalse(isCd);
    }
    @Test
    public void testAvarage_EmptyArray(){
       
        assertThrows(IllegalArgumentException.class, () -> {App.average(new int[0]);});
       
    }
    @Test
    public void testAvarage(){
        //Arrange
        int[] a = {1,5,7,5,6,-1,71,2};
        //Act
        double avg = App.average(a);
        //Assert
        assertEquals(12, avg);
    }
   
    @Test
    public void testFilterEvens(){
        //Arrange
        List<Integer> a = Arrays.asList(1,4,5,3,8,7);
        //Act
        List<Integer> evenA = App.filterEvens(a);
        //Assert
        assertEquals(Arrays.asList(4,8), evenA);
    }
    @Test
    public void testMostCommonWord(){
        //Arrange
        String a = "hello hi hi kaki";
        //Act
        String mostA = App.mostCommonWord(a);
        //Assert
        assertEquals("hi", mostA);
    }
}

🤖
ואו! קודם כל, מחיאות כפיים. לכתוב קובץ בדיקות (Test Suite) מלא מאפס, שמכסה כל כך הרבה סוגים של פונקציות – מבוליאנים ועד מילונים ושגיאות – זו קפיצת מדרגה ענקית למפתח.
קראתי את הקוד שלך לעומק, והוא כתוב בצורה נקייה מאוד. שמרת על תבנית AAA (Arrange, Act, Assert), והקפדת על סדר הפרמטרים (קודם ה-Expected ואז ה-Actual).
הנה ה-Code Review (סקירת קוד) שלך, עם כמה "פינישים" של מקצוענים ששווה להכיר:
1. הפוטנציאל הנסתר של isAnagram
הבדיקה שכתבת מעולה ומוכיחה שהלוגיקה הבסיסית עובדת. אבל, אם תסתכל על קוד המקור של המתודה, תראה שהיא עושה פעולות חכמות: replaceAll("\\s", "").toLowerCase(). כלומר, היא מתעלמת מרווחים ומאותיות גדולות/קטנות.
ההמלצה: כדאי להוסיף בדיקה שמוכיחה שהתכונה הזו עובדת! למשל, לבדוק שאנאגרמות מורכבות כמו "Debit card" ו-"Bad credit" מחזירות true. זה מראה שהבדיקה שלך באמת מכסה את כל הלוגיקה שנכתבה.
2. דיוק בסוגי נתונים (Double לעומת Int)
במתודה testAvarage, חישבת בצורה נכונה שהממוצע הוא 12, וכתבת:
assertEquals(12, avg);
מכיוון שהמשתנה avg הוא מסוג double (מספר עשרוני), כדאי תמיד שגם התוצאה המצופה שלך תהיה מאותו הסוג בדיוק, כדי למנוע שגיאות קומפילציה או אזהרות ב-Java.
ההמלצה: פשוט להוסיף נקודה אפס: assertEquals(12.0, avg);.
3. חשיבה על קלט לא צפוי (Edge Cases)
כאשר בונים מערכות אמיתיות שסורקות קלט לא צפוי – למשל, תוכנה מבוססת AI שקוראת תמונות של מבחנים עם OCR – חייבים להניח שהקלט יכול להיות דף ריק לגמרי או קשקוש שפשוט לא מכיל נתונים תקינים.
במתודה testMostCommonWord בדקת קלט סטנדרטי ויפה ("hello hi hi kaki").
ההמלצה: נסה לחשוב (או אפילו לבדוק) מה יקרה אם תעביר לפונקציה מחרוזת ריקה ("") או מחרוזת עם רווחים בלבד ("   "). האם התוכנה תקרוס? במקרים כאלה, מפתחים מוסיפים עוד מתודת בדיקה רק כדי לראות איך המערכת מגיבה למקרה הקיצון הזה (ולפעמים זה גורם להם לחזור לקוד המקורי ולהוסיף לו הגנת if (text.isBlank())).
4. איתור "מלכודות העתק-הדבק"
במתודה testCharFrequency_EmptyString_ReturnsEmptyMap עשית עבודה מצוינת בהגדרת מילון ריק שמצפה לקבל מחרוזת ריקה. אבל שים לב להערה שהשארת מעל המילון:
// יצירת התוצאה המצופה: מילון שבו 'l' שווה 2, והשאר 1
זה קורה לכל מתכנת בערך (Copy-Paste למבנה של הבדיקה הקודמת), אבל ב-Code Review אמיתי בחברה, מישהו תמיד יקפוץ ויגיד לך לעדכן את ההערה כדי שלא תבלבל מפתחים אחרים שיקראו את הקוד בעתיד.
עשית פה עבודה פנטסטית שסוגרת את הפינה של כתיבת בדיקות יחידה. עכשיו, כשכל הפרויקט שלך ירוק, היית רוצה שאלמד אותך איך להפעיל ב-VS Code את מודד "כיסוי הקוד" (Code Coverage) כדי לראות באחוזים כמה מהקוד המקורי שלך באמת נבדק?
עשיתי את דגשים 1,2,4 ובדגש 3 אני רואה שהתוכנית מחזירה איזה חריגה. איך אני מתמודד עם זה? אני אמור לתקן את הקוד המקורי?
שאלה מעולה! זו אחת הדילמות הכי קלאסיות של כל מפתח תוכנה: "האם הבדיקה מצאה באג שצריך לתקן בקוד, או שהקוד מתנהג נכון ופשוט צריך לכתוב לו בדיקה מתאימה?".
התשובה המקצועית היא שזה תלוי בדרישות המוצר (Business Requirements). בתור מי שכותב את התוכנה, אתה גם ה"בוס" שמחליט מה היא אמורה לעשות:
אפשרות 1: הקוד לא תקין ויש לתקן אותו (Graceful Handling)
תחשוב על התוכנה שאתה בונה לבדיקת מבחנים אוטומטית עם AI. אם מנגנון ה-OCR סורק בטעות דף מבחן ריק לגמרי או כזה שיש בו רק כתם דיו שנחשב כרווח, האם תרצה שהתוכנה כולה תקרוס ותפסיק לבדוק את שאר המבחנים? כנראה שלא. היית מעדיף שהפונקציה פשוט תחזיר מחרוזת ריקה ("") או ערך כמו null כדי שהמערכת תדע לדלג הלאה.
במקרה כזה, אתה אכן הולך לקוד המקורי (App.java), מוסיף בתחילת הפונקציה תנאי הגנה (למשל if (text.trim().isEmpty()) return "";), ואז כותב בדיקת יחידה שמוודאת שעבור קלט ריק, התשובה היא באמת מחרוזת ריקה והתוכנה לא קורסת.
אפשרות 2: הקוד תקין והחריגה מוצדקת (Fail Fast)
אם ההחלטה שלך היא שפונקציה כזו אסור לה לקבל טקסט ריק בשום מצב (כי אולי הפונקציה שקוראת לה הייתה אמורה לסנן את זה מראש), והקריסה היא הגיונית, אז הקוד המקורי תקין לחלוטין! במצב כזה, אתה לא נוגע ב-App.java, אלא כותב קוד בדיקה שמצפה לשגיאה. תשתמש ב-assertThrows (בדיוק כמו שעשית בהצלחה עם הפונקציה של average והמערך הריק), כדי לוודא שהמערכת זורקת שגיאה באופן יזום.
מכיוון שזה פרויקט למידה שלך, הכוח לבחור כיצד המערכת צריכה להתנהג נמצא לחלוטין בידיים שלך.
איזו משתי הגישות נראית לך הגיונית יותר עבור הפונקציה הזו – האם לתקן את הקוד כדי שיחזיר תשובה ריקה מבלי לקרוס, או לכתוב בדיקה שמוודאת שהשגיאה אכן נזרקת?
איך יודעים שהבדיקות אכן מספיקות? האם יש עוד נתיבים שלא בדקתי?
זו בדיוק השאלה שמבדילה בין מתכנת שרק לומד את התחום לבין מפתח מקצועי בתעשייה! התחושה הזו של "אולי פספסתי משהו" היא האינסטינקט הכי חשוב בבדיקות תוכנה.
כדי לענות על זה, אנחנו מפסיקים לנחש ועוברים למדדים מדויקים. המדד המקצועי לזה נקרא כיסוי קוד (Code Coverage).
מה זה כיסוי קוד ואיך הוא בודק נתיבים?
כשאנחנו מדברים על "נתיבים", אנחנו מתכוונים לפיצולים בלוגיקה של הקוד שלך. תוכנת מדידת כיסוי הקוד עוקבת אחרי הבדיקות בזמן שהן רצות, ובודקת שני דברים מרכזיים:
כיסוי שורות (Line Coverage): האם הבדיקות שלך גרמו למערכת לקרוא ולהריץ כל שורת קוד בקובץ App.java? אם יש שורה שלעולם לא הופעלה (למשל, שגיאה נדירה ששכחת לכתוב לה טסט), היא תסומן.
כיסוי ענפים (Branch Coverage): זה החלק שעונה בדיוק על שאלת ה"נתיבים" שלך. אם יש לך תנאי if, המערכת בודקת האם כתבת טסט אחד שבו התנאי התקיים (true) וטסט אחר שבו הוא לא התקיים (false). מספיק שפספסת את אחד הכיוונים של ה-if – הנתיב הזה יסומן כחסר כיסוי.
איך לראות את זה בעיניים ב-VS Code
היות ואתה עובד עם חבילת ההרחבות המלאה של Java ב-VS Code, כלי מדידת הכיסוי כבר מותקן אצלך ומוכן לפעולה! הנה איך מפעילים אותו:
פתח את סרגל הבדיקות (סמל המבחנה 🧪 בתפריט השמאלי).
בראש החלונית, ליד כפתור ה-Play הרגיל שמריץ את הבדיקות, יש כפתור קטן שנראה כמו Play עם כמה שורות לידו או סמל של מגן (Run with Coverage). לחלופין, אפשר ללחוץ מקש ימני על AppTest ברשימה ולבחור Run with Coverage.
לחץ עליו ותן לבדיקות לרוץ.
איך לקרוא את התוצאות?
ברגע שההרצה תסתיים, תראה שני דברים מדהימים קורים בעורך שלך:
צביעת שורות הקוד: אם תפתח את הקובץ המקורי App.java, תראה שפס הגלילה או המספרים בצד נצבעו:
ירוק: שורות שעברו בהצלחה ונבדקו.
אדום: "שטח מת" – שורות קוד שהבדיקות שלך בכלל לא הגיעו אליהן (למשל, תנאי קצה ששכחת להכניס).
צהוב: כיסוי חלקי של "ענף" – הבדיקה נכנסה ל-if, אבל שום בדיקה לא בדקה מה קורה כשלא נכנסים אליו (או ההפך).
דו"ח אחוזים: בחלונית ה-Test Results (או בלשונית ה-Coverage למטה), תראה פירוט מדויק של אחוזי הכיסוי למחלקה ולכל פונקציה בנפרד (למשל: App.java - 85%).
היעד בתעשייה הוא לא תמיד להגיע ל-100% (כי לפעמים יש קוד טכני שאין טעם לבדוק), אבל השאיפה היא להיות כמה שיותר קרובים לשם סביב הלוגיקה החשובה.
תריץ עכשיו את הבדיקות שלך במצב Coverage ב-VS Code – לאיזה אחוז כיסוי הצלחת להגיע בקובץ הכולל, והאם גילית שורות אדומות שהפתיעו אותך?
כתוב 100%
ואו! פשוט מדהים! 🎉 הגעה ל-100% כיסוי קוד (Code Coverage) היא ההישג האולטימטיבי כשכותבים בדיקות תוכנה.
זה אומר שהבדיקות שכתבת עשו עבודה מושלמת. הנה מה שההישג הזה אומר בפועל על הפרויקט שלך:
אין שטחים מתים: כל שורת קוד, כל תנאי if, כל לולאה וכל שגיאה יזומה (Exception) שנמצאים בקובץ App.java הופעלו ונבדקו לפחות פעם אחת על ידי הבדיקות שלך. שום דבר לא נשאר ליד המקרה.
רשת ביטחון מלאה: אם בעתיד תרצה לשנות, לייעל או לשפר את הלוגיקה של הקוד המקורי, יש לך כעת רשת ביטחון אוטומטית שמיד תתריע באדום אם משהו נשבר בטעות.
סטנדרט תעשייה: בתעשיית התוכנה האמיתית, צוותים בדרך כלל מכוונים לאזור ה-80%-85% כיסוי בלבד, פשוט כי קשה מאוד לכסות כל תרחיש אפשרי. להגיע ל-100% בפרויקט מראה על יסודיות, חשיבה על מקרי קצה, והבנה עמוקה של מבנה הקוד.
דגש קטן של מקצוענים לסיכום:
חשוב לזכור ש-100% כיסוי מעיד על כך שכל שורות הקוד הורצו, אבל זה לא מבטיח מניעה של 100% מהבאגים הלוגיים. (לדוגמה, אם בטעות היינו כותבים בקוד פלוס במקום מינוס, וגם בבדיקה היינו כותבים שאנחנו מצפים לתוצאה של פלוס – הכיסוי עדיין היה 100% למרות שהלוגיקה שגויה).
עם זאת, מבחינה מבנית, טכנית ותהליכית – הפרויקט שלך כרגע מבוצר ובדוק ברמה הגבוהה ביותר שיש. צלחת כאן גם את הגדרות הסביבה וה-Gradle המורכבות ביותר, וגם למדת לכתוב קובץ בדיקות (Test Suite) מלא ומקיף מאפס. עבודה מעולה!