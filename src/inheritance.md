# Ժառանգում (Inheritance)

## Բովանդակություն

- [Ժառանգում (Inheritance)](#ժառանգում-inheritance)
  - [Բովանդակություն](#բովանդակություն)
  - [Ժառանգականություն - նոր տիպերի ստացում՝ ավելի մասնագիտացված վարքագիծ ստեղծելու համար](#ժառանգականություն---նոր-տիպերի-ստացում-ավելի-մասնագիտացված-վարքագիծ-ստեղծելու-համար)
  - [Աբստրակտ և վիրտուալ մեթոդներ](#աբստրակտ-և-վիրտուալ-մեթոդներ)
  - [Աբստրակտ բազային դասեր](#աբստրակտ-բազային-դասեր)
  - [Հետագա ժառանգման կանխում](#հետագա-ժառանգման-կանխում)

## Ժառանգականություն - նոր տիպերի ստացում՝ ավելի մասնագիտացված վարքագիծ ստեղծելու համար

[Inheritance - derive types to create more specialized behavior](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/object-oriented/inheritance)

Ժառանգականությունը թույլ է տալիս ստեղծել նոր դասեր, որոնք օգտագործում են, ընդլայնում և փոփոխում այլ դասերում սահմանված վարքագիծը։ Դասը, որի անդամները ժառանգվում են, կոչվում է **բազային (base) դաս**, իսկ դասը, որը ժառանգում է այդ անդամներին, կոչվում է **ածանցյալ (derived) դաս**։ Ածանցյալ դասը կարող է ունենալ միայն մեկ ուղղակի բազային դաս։ Սակայն ժառանգականությունը անցումային է։ Եթե ClassC-ն ածանցվում է ClassB-ից, իսկ ClassB-ն՝ ClassA-ից, ClassC-ն ժառանգում է ClassB-ում և ClassA-ում հայտարարված անդամները։

Ածանցյալ դասը հիմնական դասի յուրահատուկ տեսակ է: Օրինակ, եթե դուք ունեք Animal հիմնական դաս, կարող եք ունենալ մեկ ածանցյալ դաս, որը կոչվում է Mammal, և մեկ այլ ածանցյալ դաս, որը կոչվում է Reptile: Mammal-ն և Reptile-ն Animal են, սակայն հանդիսանալով ածանցյալ դասեր յուրաքանչյուրը ներկայացնում է հիմնական դասի յուրահատուկ տեսակ:

Ածանցյալ դաս ստեղծելիս, այն անուղղակիորեն ստանում է բազային դասի բոլոր անդամները, բացառությամբ դրա կոնստրուկտորների և finalizers-ների։ Ածանցյալ դասը օգտագործում է բազային դասի կոդը։ Ածանցյալ դասում հնարավոր է ավելացնել անդամներ։ Ածանցյալ դասը ընդլայնում է բազային դասի ֆունկցիոնալությունը։

Հետևյալ նկարը ցույց է տալիս WorkItem դասը, որը ներկայացնում է աշխատանքային տարր որևէ բիզնես գործընթացում: Բոլոր դասերի նման, այն ծագում է `System.Object`-ից և ժառանգում է իր բոլոր մեթոդները: `WorkItem`-ը ավելացնում է իր սեփական վեց անդամ: Այս անդամները ներառում են կոնստրուկտոր, քանի որ կոնստրուկտորները չեն ժառանգվում: `ChangeRequest` դասը ժառանգում է `WorkItem`-ից և ներկայացնում է աշխատանքային տարրի որոշակի տեսակ: `ChangeRequest`-ը ավելացնում է ևս երկու անդամ այն ​​անդամներին, որոնք ժառանգում է WorkItem-ից և Object-ից: Այն պետք է ավելացնի իր սեփական կոնստրուկտորը, և այն նաև ավելացնում է `originalItemID`: `originalItemID` հատկությունը թույլ է տալիս `ChangeRequest` օրինակին կապվել սկզբնական `WorkItem`-ի հետ, որին `ChangeRequest`-ը վերաբերում է:

![class inheritance diagram](img/class-inheritance-diagram.png)

```c#
// WorkItem-ը անուղղակիորեն ժառանգում է Object դասը։
public class WorkItem
{
    // Ստատիկ currentID դաշտը պահպանում է վերջին ստեղծված WorkItem-ի job-ի ID-ն։
    private static int currentID;

    // Հատկություններ
    protected int ID { get; set; }
    protected string Title { get; set; }
    protected string Description { get; set; }
    protected TimeSpan jobLength { get; set; }

    // Լռելյայն կոնստրուկտոր (C#-ում լռելյայն կոնստրուկտորը այնպիսի կոնստրուկտոր է, որը չունի պարամետրեր)։
    // Եթե ածանցյալ դասը բացահայտորեն չի կանչում բազային  
    // դասի կոնստրուկտոր, լռելյայն կոնստրուկտորը կանչվում է անուղղակիորեն։
    public WorkItem()
    {
        ID = 0;
        Title = "Default title";
        Description = "Default description.";
        jobLength = new TimeSpan();
    }

    // Օրինակի կոնստրուկտոր որը ունի երեք պարամետրեր
    public WorkItem(string title, string desc, TimeSpan joblen)
    {
        this.ID = GetNextID();
        this.Title = title;
        this.Description = desc;
        this.jobLength = joblen;
    }


// Ստատիկ կոնստրուկտոր՝ ստատիկ currentID անդամի ինիցիալիզացնելու համար։ Այս կոնստրուկտորը կանչվում է մեկ 
// անգամ, ավտոմատ կերպով, նախքան WorkItem-ի կամ ChangeRequest-ի որևէ օրինակի ստեղծումը կամ currentID-ին
// հղում կատարելիս։

    static WorkItem() => currentID = 0;

    // currentID-ն ստատիկ դաշտ է։ Այն ավելանում է ամեն անգամ, երբ ստեղծվում է WorkItem-ի նոր օրինակ։
    protected int GetNextID() => ++currentID;

    // Update մեթոդը թույլ է տալիս թարմացնել գոյություն ունեցող WorkItem օբյեկտի title-ն և jobLength-ը։
    public void Update(string title, TimeSpan joblen)
    {
        this.Title = title;
        this.jobLength = joblen;
    }

    // System.Object-ից ժառանգված ToString վիրտուալ մեթոդի մեթոդի փոխարինում։
    public override string ToString() =>
        $"{this.ID} - {this.Title}";
}

// ChangeRequest-ը  ժառանգում է WorkItem-ից և ավելացնում է originalItemID հատկությունը և երկու կոնստտուկտոր
public class ChangeRequest : WorkItem
{
    protected int originalItemID { get; set; }

// Կոնստրուկտորներ։ Քանի որ ոչ մի բազային դասի կոնստրուկտոր չի կանչում 
// բազային դասի լռելյայն կոնստրուկտորը կանչվում է անուղղակիորեն։ 
// Բազային դասը պետք է պարունակի լռելյայն կոնստրուկտոր։

    // Ստացված դասի լռելյայն կոնստրուկտորը։
    public ChangeRequest() { }

    // Չորս պարամետր ունեցող օրինակի կոնստրուկտոր։
    public ChangeRequest(string title, string desc, TimeSpan jobLen,
                         int originalID)
    {
        // Հետևյալ հատկությունները և GetNexID մեթոդը ժառանգվում են
        // WorkItem-ից։
        this.ID = GetNextID();
        this.Title = title;
        this.Description = desc;
        this.jobLength = jobLen;

        // originalItemID հատկությունը ChangeRequest-ի անդամ է, բայց ոչ WorkItem-ի։
        this.originalItemID = originalID;
    }
}

```

Հաջորդ օրինակը ցույց է տալիս, թե ինչպես օգտագործել բազային և ածանցյալ դասերը։

```c#
// Ստեղծվում է WorkItem-ի օրինակ՝ օգտագործելով բազային դասի կոնստրուկտորը, որը ընդունում է երեք արգումենտ։
WorkItem item = new WorkItem("Fix Bugs",
                            "Fix all bugs in my code branch",
                            new TimeSpan(3, 4, 0, 0));

// Ստեղծվում է ChangeRequest-ի օրինակ՝ օգտագործելով ածանցյալ դասի կոնստրուկտորը, որը ընդունում է չորս 
// արգումենտ։
ChangeRequest change = new ChangeRequest("Change Base Class Design",
                                        "Add members to the class",
                                        new TimeSpan(4, 0, 0),
                                        1);

// Օգտագործում ենք WorkItem-ում սահմանված ToString մեթոդը։
Console.WriteLine(item.ToString());

// Օգտագործվում է Update մեթոդը ChangeRequest օբյեկտի վերնագիրը փոխելու համար։
change.Update("Change the Design of the Base Class",
    new TimeSpan(4, 0, 0));

// ChangeRequest-ը ժառանգում է WorkItem-ի ToString մեթոդի փոխարինված տարբերակը։
Console.WriteLine(change.ToString());
/* Արդյունք:
    1 - Fix Bugs
    2 - Change the Design of the Base Class
*/
```

## Աբստրակտ և վիրտուալ մեթոդներ

[Abstract and virtual methods](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/object-oriented/inheritance#abstract-and-virtual-methods)

Երբ հիմքային դասը հայտարարում է մեթոդը որպես վիրտուալ (virtual), ժառանգվող դասը կարող է վերասահմանել այդ մեթոդը իր սեփական իրականացման միջոցով։ Եթե հիմքային դասը հայտարարում է անդամը որպես աբստրակտ (abstract), ապա այդ մեթոդը պարտադիր է վերասահմանել ցանկացած ոչ-աբստրակտ դասում, որը անմիջականորեն ժառանգվում է այդ դասից։ Եթե ժառանգվող դասը նույնպես աբստրակտ է, ապա այն ժառանգում է աբստրակտ անդամները առանց դրանց իրականացման։
Աբստրակտ և վիրտուալ անդամները հանդիսանում են բազմաձևության (polymorphism) հիմքը, որը օբյեկտակենտրոն ծրագրավորման երկրորդ հիմնական հատկանիշն է։

```c#
using System;

abstract class Animal
{
    // Աբստրակտ մեթոդները ունեն միայն ստորագրություն սակայն չունեն մարմին, որը կպարունակի իրագործումը
    public abstract void MakeSound();

    // Վիրտուալ մեթոդ լռելյայն իրագործմամբ
    public virtual void Eat()
    {
        Console.WriteLine("Eating food...");
    }

    // Ոչ աբստրակտ մեթոդ
    public void Sleep()
    {
        Console.WriteLine("Sleeping...");
    }
}

class Dog : Animal // Dog դասը ժառանգում է Animal -ից
{
    // Իրագործվում է MakeSound աբստրակտ մեթոդը
    public override void MakeSound()
    {
        Console.WriteLine("Bark");
    }

    // Փոփոխվում է բազային դասի վիրտուալ մեթոդը։ 
    public override void Eat()
    {
        Console.WriteLine("Dog is eating bones...");
    }
}

class Cat : Animal // Cat դասը նույնպես ժառանգում է Animal -ից
{
    // Իրագործվում է MakeSound աբստրակտ մեթոդը
    public override void MakeSound()
    {
        Console.WriteLine("Meow");
    }

    // Այս դասում կօգտագործվի Eat մեթոդի լռելյայն իրագործումը քանի որ այն փոփոխված չէ տվյալ դասում։
}

class Program
{
    static void Main()
    {
        Animal dog = new Dog();
        Animal cat = new Cat();

        dog.MakeSound();  // Դուրս բերվող արժեք՝ Bark
        dog.Eat();        // Դուրս բերվող արժեք՝ Dog is eating bones...
        dog.Sleep();      // Դուրս բերվող արժեք՝ Sleeping...

        cat.MakeSound();  // Դուրս բերվող արժեք՝ Meow
        cat.Eat();        // Դուրս բերվող արժեք՝ Eating food... (base implementation is used)
        cat.Sleep();      // Դուրս բերվող արժեք՝ Sleeping...
    }
}

```

## Աբստրակտ բազային դասեր

Դուք կարող եք հայտարարել դասը որպես աբստրակտ (abstract), եթե ցանկանում եք կանխել դրա անմիջական օբյեկտի ստեղծումը `new` օպերատորի միջոցով։ **Աբստրակտ դասը կարող է օգտագործվել միայն այն դեպքում, երբ նրանից ժառանգվում է նոր դաս**։

Աբստրակտ դասը կարող է պարունակել մեկ կամ մի քանի մեթոդների հայտարարություններ, որոնք ինքնին հայտարարված են որպես աբստրակտ։ Այս հայտարարությունները որոշում են մեթոդի պարամետրերը և վերադարձվող արժեքը, սակայն չեն պարունակում իրականացման մաս (մեթոդի մարմին)։

Աբստրակտ դասը պարտադիր չէ, որ պարունակի աբստրակտ անդամներ։ Սակայն, եթե դասը պարունակում է աբստրակտ անդամ, ապա հենց դասը նույնպես պետք է հայտարարվի որպես աբստրակտ։
Ցանկացած ոչ-աբստրակտ ժառանգվող դաս պարտադիր պետք է իրագործի աբստրակտ հիմքային դասի աբստրակտ մեթոդները։

## Հետագա ժառանգման կանխում

Դասը կարող է կանխել այլ դասերից իր ժառանգումը կամ իր անդամներից որևէ մեկի ժառանգումը՝ հայտարարվելով կամ իր անդամներից որևէ մեկը հայտարարվելով `sealed`։
