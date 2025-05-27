# Ջեներիքսներ (generics) և Իտերֆեյսներ

## Բովանդակություն

- [Ջեներիքսներ (generics) և Իտերֆեյսներ](#ջեներիքսներ-generics-և-իտերֆեյսներ)
  - [Բովանդակություն](#բովանդակություն)
  - [Ջեներիքսներ (generics)](#ջեներիքսներ-generics)
  - [Ինտերֆեյսներ](#ինտերֆեյսներ)

## Ջեներիքսներ (generics)

Generics-ը .NET-ում ներմուծում է **տիպի պարամետրի** հասկացությունը: Generics-ները հնարավորություն են տալիս նախագծել դասեր և մեթոդներ, որոնք հետաձգում են մեկ կամ մի քանի պարամետրերի տիպերի սահմանումը մինչև դասի կամ մեթոդի օգտագործումը:

```c#
using System;
using System.Collections.Generic;

// Սահմանում ենք ջեներիք դաս
public class GenericList<T>
{
    // դաշտ որի տիպն է T տեսակի ցուցակ (list)
    private List<T> items = new List<T>();

    // Տվյալ մեթոդը ավելացնում է էլեմենտ items ցուցակում։ Ելեմենտը պետք է լինի T տեսակի
    public void Add(T item)
    {
        items.Add(item);
        Console.WriteLine($"{item} added to the list.");
    }

    public void DisplayAll()
    {
        Console.WriteLine("List contents:");
        foreach (var item in items)
        {
            Console.WriteLine(item);
        }
    }
}

public class ExampleClass
{
    public string Name { get; set; }

    public ExampleClass(string name)
    {
        Name = name;
    }

    public override string ToString()
    {
        return Name;
    }
}

class Program
{
    static void Main()
    {
        // Ստեղծվում է GenericList տիպի դաս int տիպի ջեներիք պարամետրով
        GenericList<int> intList = new();
        intList.Add(10); // Փոխանցվում է int արժեք, որը համապատասխանում է T տիպին
        intList.Add(20); // Փոխանցվում է int արժեք, որը համապատասխանում է T տիպին
        intList.DisplayAll();

        Console.WriteLine();

        // Ստեղծվում է GenericList տիպի դաս string տիպի ջեներիք պարամետրով
        GenericList<string> stringList = new();
        stringList.Add("Hello");  // Փոխանցվում է string, արժեք որը համապատասխանում է T տիպին
        stringList.Add("World"); // Փոխանցվում է string, արժեք որը համապատասխանում է T տիպին
        stringList.DisplayAll();

        Console.WriteLine();

        // Ստեղծվում է GenericList տիպի դաս ExampleClass տիպի ջեներիք պարամետրով
        GenericList<ExampleClass> objectList = new();
        objectList.Add(new ExampleClass("Object 1")); // Փոխանցվում է ExampleClass, արժեք որը համապատասխանում է T տիպին
        objectList.Add(new ExampleClass("Object 2")); // Փոխանցվում է ExampleClass, արժեք որը համապատասխանում է T տիպին
        objectList.DisplayAll();
    }
}

```

## Ինտերֆեյսներ

Ինտերֆեյսը պարունակում է փոխկապակցված ֆունկցիոնալությունների խմբի սահմանումներ, որոնք պետք է իրականցնի ոչ աբստրակտ դասը կամ կառուցվածքը (struct): Ինտերֆեյսը կարող է սահմանել ստատիկ մեթոդներ, որոնք պետք է իրականացում ունենան: Ինտերֆեյսը կարող է սահմանել անդամների համար լռելյայն իրականացում: Ինտերֆեյսը չի կարող հայտարարել օրինակի տվյալներ, ինչպիսիք են դաշտերը, ավտոմատ կերպով իրականացվող հատկությունները:

Ինտերֆեյսը սահմանվում է օգտագործելով `interface` բանալի բառը, ինչպես ցույց է տրված հետևյալ օրինակում։

```c#
interface IEquatable<T>
{
    bool Equals(T obj);
}
```

IEquatable<T> ինտերֆեյսը իրականացնող ցանկացած դաս կամ կառուցվածք պետք է պարունակի Equals մեթոդի սահմանում, որը համապատասխանում է ինտերֆեյսի կողմից նշված ստորագրությանը: Արդյունքում, դուք կարող եք հույս դնել IEquatable<T> իրականացնող T տիպի դասի վրա, որը պարունակում է Equals մեթոդ, որի միջոցով այս դասի մեկ օրինակ կարող է որոշել, թե արդյոք այն հավասար է նույն դասի մեկ այլ օրինակի, թե ոչ:

IEquatable<T>-ի սահմանումը չի ներառում Equals-ի իրականացումը: Դասը կամ կառուցվածքը կարող են իրականացնել բազմաթիվ ինտերֆեյսներ, բայց դասը կարող է ժառանգել միայն մեկ դասից:

**Ինտերֆեյսները կարող են պարունակել օրինակների (instance) մեթոդներ, հատկություններ, իրադարձություններ, ինդեքսատորներ** կամ այդ չորս անդամների ցանկացած համակցություն։ Ինտերֆեյսները **կարող են պարունակել ստատիկ կոնստրուկտորներ, դաշտեր, հաստատուններ կամ օպերատորներ**։ C# 11-ից սկսած, ինտերֆեյսի այն անդամները, որոնք դաշտեր չեն, կարող են լինել ստատիկ աբստրակտ։ **Ինտերֆեյսը չի կարող պարունակել օրինակների դաշտեր, օրինակների կոնստրուկտորներ**։ Ինտերֆեյսի անդամները լռելյայն public են: Հնարավոր է սահմանել նաև այլ հասանելիության մոդիֆիկատորները, ինչպիսիք են՝ public, protected, internal, private, protected internal կամ private protected։ Private անդամը պետք է ունենա լռելյայն իրականացում։

Ինտերֆեյսի անդամը իրականացնելիս, իրականացնող դասի համապատասխան անդամը պետք է լինի public, ոչ ստատիկ և ունենա նույն անունն ու ստորագրությունը, ինչ ինտերֆեյսի անդամը։

>[!NOTE]
> Երբ ինտերֆեյսը հայտարարում է ստատիկ անդամներ, այն տիպը, որը իրականացնում է այդ ինտերֆեյսը, կարող է նաև
> հայտարարել նույն ստորագրությամբ ստատիկ անդամներ։ Դրանք տարբերվում են և նույնականացվում են այն տիպով, որը
> հայտարարում է անդամը։ Տիպում հայտարարված ստատիկ անդամը չի գերբեռնում (override) ինտերֆեյսում հայտարարված ստատիկ անդամին։

```c#
public interface IExample
{
    static void Display() => Console.WriteLine("Interface Static Method");
}

public class ExampleClass : IExample
{
    public static void Display() => Console.WriteLine("Class Static Method");
}

class Program
{
    static void Main()
    {
       IExample.Display();  // Կանչում է ինտերֆեսի ստատիկ մեթոդը

       ExampleClass.Display();  // Կանչում է դասի ստատիկ մեթոդը
    }
}
```

Ինտերֆեյսը իրականացնող դասը կամ կառուցվածքը (struct) պետք է իրագործի ինտերֆեյսի կողմից տրամադրված բոլոր հայտարարված անդամները, որոնք չունեն լռելյայն իրականացում։ Եթե բազային դասը իրականացնում է ինտերֆեյսը, ապա այդ բազային դասի ցանկացած ածանցյալ դաս կժառանգի այդ իրականացումը։

Հետևյալ օրինակը ցույց է տալիս IEquatable<T> ինտերֆեյսի իրականացումը։ Իրականացնող Car դասը պետք է ապահովի Equals մեթոդի իրականացումը։

```c#
public class Car : IEquatable<Car>
{
    public string? Make { get; set; }
    public string? Model { get; set; }
    public string? Year { get; set; }

    // IEquatable<T> ինետրֆեյսի շրջանակում իրագործվում է Equals մեթոդը
    public bool Equals(Car? car)
    {
        return (this.Make, this.Model, this.Year) ==
            (car?.Make, car?.Model, car?.Year); // ատուգվում է փոխանցված և ընթացիկ դասի՝ Make, Model և Year հատկությունների համապատասխանությունը
    }
}
```
