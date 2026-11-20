- C# microsoft trarafından .Net altyapısı kullanarak ayağa kaldırılan ve tamamen nesne tabanlı çalışan bir dildir.
- Genel bir c# yapısını inceleyelim 
```c#
```csharp
using System; // Burası sistem kütüphanesini ekleyen kısımdır 

namespace HelloWorld // Programın adı 
{
  class Program // programın genel nesnesi 
  {
    static void Main(string[] args) //
    {
      Console.WriteLine("Hello World!");    
    }
  }
}
```

> Static Void Main
> Static bir anahtar kelimedir aslında. Değişken oluşturulurken ayrı bir sınıf gerekmediğini belirtir.
> Void : Bu fonksiyon çalıştıktan sonra geriye bir şey döndürmeyeceğini söyler 


### DEĞİŞKENLER 
- Değişken oluştururken;
 ```c#
 type + variableName =Value; 
 ```

- Genel kullandığımız anahtar kelimelerde bunların başına gelmektedir.( Const , atomic , static gibi )
```c#
  csharp
int myNum = 5;               // Integer (whole number)
double myDoubleNum = 5.99D;  // Floating point number
char myLetter = 'D';         // Character
bool myBool = true;          // Boolean
string myText = "Hello";     // String
```

| Data type | size                  | Description                                                                       |
| --------- | --------------------- | --------------------------------------------------------------------------------- |
| `int`     | 4 bytes               | Stores whole numbers from -2,147,483,648 to 2,147,483,647                         |
| `long`    | 8 bytes               | Stores whole numbers from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| `float`   | 4 bytes               | Stores fractional numbers. Sufficient for storing 6 to 7 decimal digits           |
| `double`  | 8 bytes               | Stores fractional numbers. Sufficient for storing 15 decimal digits               |
| `bool`    | 1 byte                | Stores true or false values                                                       |
| `char`    | 2 bytes               | Stores a single character/letter, surrounded by single quotes                     |
| `string`  | 2 bytes per character | Stores a sequence of characters, surrounded by double quotes                      |
### TÜR DÖNÜŞÜMLERİ 
-  Burda to diye bi anahtar kelime kullanıyoruz 
- 
```c#
```csharp
int myInt = 10;
double myDouble = 5.25;
bool myBool = true;

Console.WriteLine(Convert.ToString(myInt));    // convert int to string
Console.WriteLine(Convert.ToDouble(myInt));    // convert int to double
Console.WriteLine(Convert.ToInt32(myDouble));  // convert double to int
Console.WriteLine(Convert.ToString(myBool));   // convert bool to string
```
GetType metodu ile verilerin tipini öğrenebilirsiniz 
![[Pasted image 20260219001748.png]],
Burda enteresandır parantezlerde birer metod sayılmaktadır. Burda parantez koymasaydık sistemdeki string adreslemesini çıktı olarak alırdık 

### KULLANICI GİRİŞİ 
- ConsoloWrite ile yazdırırken ConsoleReadLine ile okuycaz basit

```csharp
// Type your username and press enter
Console.WriteLine("Enter username:");

// Create a string variable and get user input from the keyboard and store it in the variable
string userName = Console.ReadLine();

// Print the value of the variable (userName), which will display the input value
Console.WriteLine("Username is: " + userName);
```
-  Aslında tür dönşümlerini sadece burda kulancaz :D Boşuna öğrendik saygılar...

### MATEMATİK MODÜLÜ 

- Math.{metod} ile kullanılır 
``` c#
Math.Max // parametrelerden en büyüğünü seçer 
Math.Min // en küçük 
Math.Sqrt // Ortalama alır 
Math. Abs // Mutlak değeri alır 
Math.Round // Yuvarlar 

```

### DİZİ OLUŞTURMA 
Buda basit aq izle 

```c#
string [] cars= {"Volvo","BMW","Ford","Mazda"};
```
 bu iste 
veya 

```c#
int [] sayi = {10,20,40};
```

-  Her dilde olduğu gibi bunlarada indexler ile erişip bölebiliyoruz 
#### İşi Büyütelim 
```c#
```csharp
// Create an array of four elements, and add values later
string[] cars = new string[4];

// Create an array of four elements and add values right away 
string[] cars = new string[4] {"Volvo", "BMW", "Ford", "Mazda"};

// Create an array of four elements without specifying the size 
string[] cars = new string[] {"Volvo", "BMW", "Ford", "Mazda"};

// Create an array of four elements, omitting the new keyword, and without specifying the size
string[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
```


![[Pasted image 20260219005044.png]]