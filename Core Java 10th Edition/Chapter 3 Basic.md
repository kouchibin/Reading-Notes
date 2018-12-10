# Chapter 3
## 3.5 Operators
- power : ```Math.pow(a, b);```
- ```import static java.lang.Math.*;``` to avoid typing ```Math.*``` each time.
- round: ```Math.round(x);```
- Java cannot cast between boolean values and any numeric type.
- Bitwise Operators
    - & and
    - | or
    - ^ xor
    - ~ not
    - use ```0b101001``` to represent binary values.
    - & and | can be applied to boolean values, but not evaluated in "short circuit" fashion.
    - ```<<``` ```>>``` bit shift
    - ```>>>``` fills the left most bit with 0, while ```>>``` preserve the sign bit.
- Enumerated Types
    ```
    enum Size {SMALL, MEDIUM, LARGE, X_LARGE};
    Size s = Size.MEDIUM;
    ```
## 3.6 Strings

- Substring: ```s.substring(0, 3);```
- Concatenation: 
    - use "+"
    - String + other, other will be converted to String
    - String.join(" / ", "S", "M", "L", "XL") - "S / M / L / XL"
- Strings are immutable
- Test Strings for Equality: 
    - ```s.equals(t)```
    - ```s.equalsIgnoreCase(t)```
    - Don't use ```==```, it test if two strings are stored in the same location.
- Get length: ```s.length()```
- Get char: ```s.charAt(i)```
- Building Strings:
```
StringBuilder sb = new StringBuilder();
sb.append(ch);
sb.append(str);
String completedString = sb.toString();
```
## 3.7 Input and Output
- Reading Input:
```
Scanner in = new Scanner(System.in);
String nextline = in.nextLine();
String firstName = in.next();
int age = in.nextInt();
```
- Reading passwords:
```
Console cons = System.console();
String username = cons.readLine("User name:");
char[] passwd = cons.readPassword("Password:");
```
- Formatting Output:
```
System.out.printf("%d %s", intv, string);
String message = String.format("%d %s", intv, string);

```
- File Input and Output:
```
Scanner in = new Scanner(Paths.get("myfile.txt"), "UTF-8");
PrintWriter out = new PrintWriter("myfile.txt", "UTF-8");
out.println("***");
```
## 3.8 Control Flow
- Block Scope: Java doesn't allow redefining same variable in the nested block. This is to avoid programming errors.

## 3.9 Big Numbers
- Use java.math.BigInteger and BigDecimal

## 3.10 Array
- Get length: 
```
int[] a = new int[100];
int len = a.length;
```
- Cannot change array size after creation.
- Foreach loop:
```
// a is an array or class that implements Iterable interface
for (int element : a)
    System.out.println(element);
```
- Array Initializers and Anonymous Arrays:
```
int[] smallPrimes = { 2, 3, 5, 7, 11, 13 };
smallPrimes = new int[] { 17, 19, 23, 29, 31, 37 };
```
- Array copying:
```
int[] luckyNumbers = smallPrimes; luckyNumbers[5] = 12; // now smallPrimes[5] is also 12

int[] copiedLuckyNumbers = Arrays.copyOf(luckyNumbers, luckyNumbers.length);

// Increase the size of the array
luckyNumbers = Arrays.copyOf(luckyNumbers, 2 * luckyNumbers.length);
```
- Java array is essentially the same as a pointer to an array allocated on the heap (in C++).
- Command-Line Parameters: args[] does not contains the program name.
- Array Sorting:
```
int[] a = new int[1000];
Arrays.sort(a);
```
- Print two-dimensional array:
```
System.out.println(Arrays.deepToString(a));
```
- Ragged Array
```
int[][] odds = new int[NMAX + 1][];
for (int n = 0; n <= NMAX; n++)
    odds[n] = new int[n + 1];
    
for (int n = 0; n < odds.length; n++) 
    for (int k = 0; k < odds[n].length; k++) {
        odds[n][k] = lotteryOdds; 
    }
```