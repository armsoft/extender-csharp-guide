# Դասեր

## Բովանդակություն

- [Դասեր](#դասեր)
  - [Բովանդակություն](#բովանդակություն)
  - [Դասերի ներածություն](#դասերի-ներածություն)
    - [Հղման տեսակներ (Reference types)](#հղման-տեսակներ-reference-types)
  - [Դասերի հայտարարում](#դասերի-հայտարարում)
  - [Օբյեկտների ստեղծում](#օբյեկտների-ստեղծում)
  - [Դաշտեր (Fields) և հատկություններ (Properties)](#դաշտեր-fields-և-հատկություններ-properties)
    - [Դաշտեր](#դաշտեր)
    - [Հատկություններ](#հատկություններ)
      - [Ավտոմատ կերպով իրագործված հատկություններ](#ավտոմատ-կերպով-իրագործված-հատկություններ)
      - [Ստատիկ և միայն ընթերցման հատկությունների օրինակ](#ստատիկ-և-միայն-ընթերցման-հատկությունների-օրինակ)
  - [Կոնստրուկտորներ և ինիցիալիզացիա (Constructors and initialization)](#կոնստրուկտորներ-և-ինիցիալիզացիա-constructors-and-initialization)
  - [Մեթոդներ (Methods)](#մեթոդներ-methods)
    - [Մեթոդի ստորագրությունը (Method signatures)](#մեթոդի-ստորագրությունը-method-signatures)
    - [Մեթոդի հասանելիություն (Method access)](#մեթոդի-հասանելիություն-method-access)
    - [Մեթոդի պարամետրեր և արգումենտներ (Method parameters vs. arguments)](#մեթոդի-պարամետրեր-և-արգումենտներ-method-parameters-vs-arguments)
    - [Արժեքների և հղումների փոխանցում (Passing by reference vs. passing by value)](#արժեքների-և-հղումների-փոխանցում-passing-by-reference-vs-passing-by-value)
    - [Վերադարձվող արժեքներ](#վերադարձվող-արժեքներ)
    - [Async մեթոդներ](#async-մեթոդներ)
  - [Հասանելիության մոդիֆիկատորներ (Access Modifiers)](#հասանելիության-մոդիֆիկատորներ-access-modifiers)

## Դասերի ներածություն

### Հղման տեսակներ (Reference types)

Որպես դաս սահմանված տեսակը հղման տեսակ է։ Հղման տիպի փոփոխական հայտարարելիս, փոփոխականը պարունակում է **null** արժեքը քանի դեռ դուք չեք ստեղծել դասի օրինակ՝ օգտագործելով **new** օպերատորը, կամ վերագրել դրան արդեն ստեղծված համատեղելի տիպի օբյեկտ։

```c#
MyClass mc; // պարունակում է null արժեքը

// Հայտարարում ենք MyClass տեսակի նոր օբյեկտ 
MyClass mc1 = new MyClass();

//Հայտարարում ենք նույն տեսակի ևս մեկ փոփոխական և վերագրում ենք նրան առաջին օբյեկտը
MyClass mc2 = mc;

```

Երբ օբյեկտը ստեղծվում է, նրա համար հատկացվում է անհրաժեշտ հիշողություն ծավալը իսկ փոփոխականին փոխանցվում է տվյալ օբյեկտի հիշողության մեջ գտնվելու վայրի հղումը։

## Դասերի հայտարարում

Դասերը հայտարարվում են class բանալի բառի (keyword) և ունիկալ նույնականացուցիչի միջոցով։

```c#
//[access modifier] - [class] - [identifier]
public class Customer
{
   // դաշտեր, հատկություններ, մեթոդներ և իրադարձություններ (events)...
}

```

**class** բանալի բառից առաջ կարող է լինել հասանելիության մոդիֆիկատոր (access modifier), որի լռությամբ արժեքը **internal** է։ Քանի որ այս դեպքում օգտագործվում է public, հասանելիության մոդիֆիկատորը, յուրաքանչյուրը կարող է ստեղծել այս դասի օրինակներ։ Դասի անունը հաջորդում է **class** բանալի բառին։ Ձևավոր փակագծերում գրվող մասը դասի մարմինն է, որտեղ սահմանվում է տվյալ դասի վարքագիծը և տվյալները։ **Դասի դաշտերը, հատկությունները, մեթոդները և իրադարձությունները միասին անվանում են դասի անդամներ**։

## Օբյեկտների ստեղծում

Չնայած երբեմ **դաս** և **օբյեկտ** բարերը օգտագործվում են նույն իմաստով, **դասը** և **օբյեկտը** տարբեր բաներ են: **Դասը** սահմանում է օբյեկտի տեսակ, բայց այն ինքնին օբյեկտ չէ: Օբյեկտը դասի վրա հիմնված կոնկրետ օրինակ է:

Օբյեկտները կարող են ստեղծվել՝ օգտագործելով **new** բանալի բառը, որին հաջորդում է դասի անունը։

```c#
Customer object1 = new Customer();

```

Երբ ստեղծվում է դասի օրինակ, վերադարձվում է օբյեկտի հղումը։ Նախորդ օրինակում object1-ը հղում է դեպի օբյեկտ, որը հիմնված է Customer դասի-ի վրա։ Այս հղումը վերաբերում է նոր օբյեկտին, բայց չի պարունակում օբյեկտի տվյալները։ Փաստորեն, դուք կարող եք ստեղծել օբյեկտի հղում առանց օբյեկտ ստեղծելու։

```c#
Customer object2;
```

Խորհուրդ չի տրվում ստեղծել օբյեկտի հղումներ, որոնք չեն հղվում որոշակի օբյեկտի, քանի որ նման հղումով օբյեկտին հասանելիության փորձը, ծրագրի աշխատանքի ժամանակ կբերի սխալի:

```c#
Customer object3; // խորհուրդ չի տրվում

Customer object3 = new Customer();
Customer object4 = object3;
```

Օրինակի երկրորդ և երրորդ տողերում ստեղծում է երկու օբյեկտի հղումներ, որոնք երկուսն էլ վերաբերում են նույն օբյեկտին։ Հետևաբար, object3-ի միջոցով օբյեկտում կատարված ցանկացած փոփոխություն կարտացոլվի object4-ում։

Դասերի վրա հիմնված օբյեկտները հայտնի են որպես **հղումային տեսակներ**։

## Դաշտեր (Fields) և հատկություններ (Properties)

### Դաշտեր

Դաշտը ցանկացած տիպի փոփոխական է, որը հայտարարվում է անմիջապես դասում: Դաշտերը հանդիսանում են **դասի անդամներ**:

Դասը կարող է ունենալ **օրինակի** (instance) դաշտեր, **ստատիկ** (static) դաշտեր կամ երկուսն էլ։ Օրինակի դաշտերը պատկանում եմ տվյալ տիպի օրինակին (instance)։ Եթե դուք ունեք T դաս, F օրինակի դաշտով կարող եք ստեղծել T տիպի երկու օբյեկտ և փոփոխել F-ի արժեքը յուրաքանչյուր օբյեկտում՝ առանց ազդելու մյուս օբյեկտի արժեքի վրա։ Ի տարբերություն **ստատիկ դաշտի**, որը պատկանում է հենց դասին և օգտագործվում է այդ տիպի բոլոր օրինակների կողմից։ Դուք կարող եք հասանելիություն ունենալ **ստատիկ դաշտին** միայն տիպի անվան միջոցով։ Ստատիկ դաշտին օրինակի անունով հասանելիություն ստանալու փորձ կատարելու դեպքում, կառաջանա սխալ։

Օրինակի դաշտին հասանելիության համար, օրինակի անունից հետո պետք է ավելացնել կետ, որին հաջորդում է դաշտի անվանումը՝ **instancename._fieldName**։ Ստատիկ դաշտերի դեպքում օրինակի անունի փոխարեն գրվում է դասի անունը։

Սովորաբար դաշտերի համար սահմանում են [**private** և **protected** հասանելիություն (access modfier)](#հասանելիության-մոդիֆիկատորներ-access-modifiers): Այս դեպքում դաշտերը հասանելի չեն լինի տվյալ դասը օգտագործող կոդի համար։

```c#
// Սահմանում ենք Account դասը
class Account 
{
   // հայտարարում ենք AccountNumber string տիպի դաշտը
   private string AccountNumber = "99900012312321";
}

class Program
{
    static void Main()
    {
        // Account դասը օգտագործող կոդի համար AccountNumber դաշտը հասանելի չէ քանի որ այն ունի private հասանելիության մոդիֆիկատոր
        Account acc = new Account();
        acc.AccountNumber = "9990012362123212"; // սխալ, AccountNumber -ը հասանելի չէ
    }
  }
```

Այս դեպքում դասի տվյալների, հասանելիությունը այն օգտագործող կոդի համար, իրականացվում է մեթոդների, հատկությունների միջոցով: Ներքին դաշտերին անուղղակի հասանելիություն ունենալու դեպքում դուք կարող եք պաշտպանվել սխալ մուտքային արժեքներից:

Դաշտերում սովորաբար պահում են այն տվյալները, որոնք պետք է հասանելի լինեն դասի մեկից ավելի մեթոդների համար։

Փոփոխականները, որոնք չեն օգտագործվում մեկ մեթոդի շրջանակից դուրս, պետք է հայտարարվեն, որպես լոկալ փոփոխականներ մեթոդի մարմնում։

[Fields (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/fields)

### Հատկություններ

Օբյեկտի օգտատիրոջ համար հատկությունը նման է դաշտի. հատկության հասանելիության համար պահանջում է նույն շարահյուսությունը ինչ դաշտերի դեպքում ՝ **օբյեկտի_անուն.հատկության_անուն**:

Դասը ստեղծողի համար հատկությունը մեկ կամ երկու կոդի բլոկ է, որոնք ներկայացնում են **get** accessor-ի և/կամ **set** կամ **init** accessor-ները:

**Get** accessor-ի կոդի բլոկը կատարվում է, երբ հատկությունը ընթերցվում է. **set** կամ **init** accessor-ների կոդի բլոկերը կատարվում է, երբ հատկությանը տրվում է արժեք:

 **Set** accessor չունեցող հատկությունը համարվում է միայն ընթերցման համար: **Get** accessor չունեցող հատկությունը համարվում է միայն գրելու համար:

 Երկու accessor-ներ ունեցող հատկությունը հնարավոր է կարդալ և փոփոխել: Դուք կարող եք օգտագործել **init** accessor-ը **set** accessor-ի փոխարեն, որպեսզի հատկությանը արժեք սահմանելը լինի որպես օբյեկտի ինիցիալիզացիայի (ստեղծման) մաս, հետագայում ​​դարձնելով նրան միայն ընթերցման համար:

Հատկությունները բազմաթիվ կիրառություններ ունեն.

- կարող են ստուգել տվյալները՝ փոփոխություն կատարելուց առաջ (վալիդացիա)
- կարող են թափանցիկ կերպով արտահայտել տվյալներ վերցված են որևէ այլ աղբյուրից, օրինակ՝ տվյալների բազայից
- կարող են որոշակի գործողություններ կատարել, երբ տվյալները փոխվում են, օրինակ՝ այլ դաշտերի արժեքի փոփոխություն։

```c#
public class Date
{
    private int _month = 7;  // Backing store

    public int Month
    {
        get => _month; // Month հատկությունը կարդալիս կվերադարձվի _month դաշտի արժեքը։
        set
        {
            if ((value > 0) && (value < 13)) // արժեքի վերագրումը տեղի կունենա միայն այն դեպքում երբ այն 1-12 միջակայքում է (վալիդացիա)
            {
                _month = value;
            }
        }
    }
}

```

Այս օրինակում Month-ը հայտարարվում է որպես հատկություն, որպեսզի **set** accessor-ի միջոցով հնարավոր լինի ստուգել, որ Month-ին փոխանցվող արժեքը սահմանված է 1-ից 12 միջակայքում: Month հատկությունը օգտագործում է **private** _month դաշտը՝ արժեքը պահպանելու համար: Հատկության տվյալների իրական գտնվելու վայրը հաճախ անվանում են հատկության «պահեստ» ("backing store."):  

Դաշտը նշվում է որպես **private** որպեսզի նրա փոփոխությունը հնարավոր լինի միայն հատկությունը կանչելով:

Ավտոմատ կերպով իրականացվող հատկությունները ապահովում են պարզեցված շարահյուսություն պարզ հատկությունների հայտարարության համար:

#### Ավտոմատ կերպով իրագործված հատկություններ

```c#
public class Person
{
    public string? FirstName { get; set; }

}
```

Վերևի օրինակը ցույց է տալիս ավտոմատ կերպով իրագործված հատկություն։ Կոմպիլյատորը ստեղծում է հատկության համար private **backing store** դաշտ, ինչպես նաև իրականացնում է **get** և **set** accessor-ների մարմինը։

**get** -ը այստեղ փաստացի ֆունկցիա է, որը վերադարձնում է ավտոմատ ստեղծված **private FirstName** դաշտի արժեքը, իսկ **set**-ը արժեք է վերագրում այդ դաշտին։

```c#
public class Person
{
    public string? FirstName
    {
        get;
        set => field = value.Trim(); // FirstName հատկությանը արժեք վերագրելիս կհեռացվեն բացատները տեղի սկզբից և վերջից
    }
}
class Program
{
    static void Main()
    {
        Person pr = new Person();
        pr.FirstName = "Armen  "; // կհեռացվեն բացատները

        Console.WriteLine(pr.FirstName); // դուրս կբերվի "Armen" բառը առանց բացատների

    }
}

```

> [!IMPORTANT]
> field բանալի բառը C# 13-ում preview հնարավորություն է: field բանալի բառն օգտագործելու համար դուք պետք է օգտագործեք .NET 9 և ձեր LangVersion տարրը պետք է կարգավորված լինի նախադիտման ռեժիմով:

```html
<LangVersion>preview</LangVersion>*
```

#### Ստատիկ և միայն ընթերցման հատկությունների օրինակ

Employee դասի օրինակին (instance) հնարավոր է փոխանցել այնուհետև կարդալ աշխատակցի անունը, ինչպես նաև ստանալ
տվյալ դասի միջոցով ստեղծված օրինակների (աշխատակիցների) քանակը։  

```c#
    public class Employee
    {
        public static int NumberOfEmployees; // ստատիկ դաշտը վերաբերում է դասին այլ ոչ թե օրինակին (instance) 
        private static int _counter; // private հասանելիության մոդիֆիկատորի շնորհիվ այն հասանելի չէ դասի վրայից
        private string _name;

        // Օրինակի (instance) գրելու և կարդալու համար հասանելի հատկություն:
        public string Name
        {
            get => _name;
            set => _name = value;
        }

        // Միայն կարդալու հատկություն (բացակայում է set accessor-ը )։ Վերադարձնում է _counter դաշտի արժեքը։
        public static int Counter => _counter; // կրճատ գրելաձև

        // Կոնստրոիկտոր
        public Employee() => _counter = ++NumberOfEmployees; // Ավելացնում է աշխատակիցների քանակը նոր օբյեկտ ստեղծելիս
    }
    class Program
    {
        static void Main()
        {
            Employee.NumberOfEmployees = 15; // Սահմանվում է աշխատակիցների քանակի սկզբնական արժեքը
            Employee e1 = new Employee();
            Employee e2 = new Employee();


            e1.Name = "Armen"; 
            e2.Name = "Anna";
            
            Console.WriteLine(e1.Name); // դուրս կբերվի "Armen"
            Console.WriteLine(e1.Name); // դուրս կբերվի "Anna"

            Console.WriteLine(Employee.Counter); // 17 
        }
    }
```

## Կոնստրուկտորներ և ինիցիալիզացիա (Constructors and initialization)

[Constructors and initialization](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/classes#constructors-and-initialization)

Նախորդ բաժիններում ներկայացվեց դասի տեսակը հայտարարելու և այդ տեսակի օրինակ ստեղծելու շարահյուսությունը: Երբ դուք ստեղծում եք տեսակի օրինակ, դուք պետք է համոզվեք, որ դրա դաշտերը և հատկությունները ինիցիալիզացվում են անհրաժեշտ արժեքներով: Արժեքները ինիցիալիզացնելու մի քանի եղանակ կա.

- Ընդունել լռելյայն արժեքներ
- Դաշտի ինիցիալիզատորներ
- Կոնստրուկտորի պարամետրեր
- Օբյեկտի ինիցիալիզատորներ

Յուրաքանչյուր .NET տիպ ունի լռելյայն արժեք: Սովորաբար այդ արժեքը 0 է թվային տիպերի համար և null՝ բոլոր հղման տիպերի համար:

Երբ անհրաժեշտ է սահմանել .NET լռելյայն արժեքից տարբեր արժեք, կարող եք օգտագործել **դաշտի ինիցիալիզատոր** .

```c#
public class Container
{
    // Սահմանվում է capacity դաշտի լռությամբ արժեքը (10):
    private int _capacity = 10;
}

```

Հնարավոր է պարտադրել, որպեսզի սկզբնական արժեքը սահմանվի կանչողի կողմից, սահմանելով կոնստրուկտոր, որը պատասխանատու է այդ սկզբնական արժեքը սահմանելու համար։

```c#
public class Container
{
    private int _capacity;

    /*Կոնստրուկտորը ֆունկցիա է, որը կրում է դասի անունը և ավտոմատ կերպով կանչվում է, երբ դասի հիման վրա օբյեկտ է ստեղծվում։
    Տվյալ դեպքում օբյեկտի ինիցիալիզացիայի ժամանակ փոխանցված պարամետրի արժեքը կվերագրվի նոր ստեղծվող օբյեկտի _capacity դաշտին։
     */
    public Container(int capacity) => _capacity = capacity; // դաշտին վերագրվում է պարամետրի արժեքը
}
 class Program
 {
     static void Main()
     {
         Container c1 = new Container(250); 
     }
 }

```

Սկսած C# 12-ից, հասանելի է կրճատ գրելաձև, որտեղ կոնստրուկտորի պարամետրները նկարագրվում են որպես դասի հայտարարության մաս։

```c#
public class Container(int capacity) // Կոնստրուկտորի պարամետրերը սահմանվում են անմիջապես դասը անվանումից հետո, վերագրման ավտոմատ կատարմամբ։
{
    private int _capacity = capacity; // կատարվում է _capacity դաշտի ինիցիալիզացիա։
}
```

Դուք կարող եք նաև օգտագործել **required** մոդիֆիկատորը հատկության վրա թույլ տալով օգտագործել օբյեկտի ինիցիալիզատոր՝ հատկության սկզբնական արժեքը սահմանելու համար։

```c#
public class Person
{
    public required string LastName { get; set; }
    public required string FirstName { get; set; }
}
```

**required** բանալի բառի ավելացումը պարտադրում է,որպեսզի սահմանվեն այդ հատկությունները որպես **new** արտահայտության մաս՝

```c#
var p1 = new Person(); // Կառաջանա սխալ, պահանջվող հատկություները սահմանված չեն
var p2 = new Person() { FirstName = "Grace", LastName = "Hopper" };

```

## Մեթոդներ (Methods)

[Methods (C# Programming Guide)](#https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods)

Մեթոդը կոդի բլոկ է, որը պարունակում է մի շարք հրամաններ։ Ծրագիրը կատարում է հրամանները կանչելով մեթոդը և նշելով մեթոդի անհրաժեշտ արգումենտները։ C#-ում յուրաքանչյուր կատարված հրահանգ կատարվում է մեթոդի համատեքստում։

Main մեթոդը յուրաքանչյուր C# ծրագրի մուտքի կետն է և այն կանչվում է Common Language Runtime (CLR)-ի կողմից, երբ ծրագիրը մեկնարկվում է։

### Մեթոդի ստորագրությունը (Method signatures)

[Method signatures](#https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods#method-signatures)

Մեթոդները հայտարարվում են դասում, կառուցվածքում(struct) կամ ինտերֆեյսում(interface)՝ նշելով հասանելիության մոդիֆիկատորը, ինչպիսիք են՝ **public** կամ **private**, լրացուցիչ մոդիֆիկատորները, ինչպիսիք են՝ **abstract** կամ **sealed**, վերադարձվող արժեքը, մեթոդի անունը և մեթոդի ցանկացած պարամետր։ Այս մասերը միասին կազմում են մեթոդի ստորագրությունը։

Մեթոդի պարամետրերը գրվում են փակագծերի մեջ և բաժանվում են ստորակետերով: Դատարկ փակագծերը ցույց են տալիս, որ մեթոդը պարամետրեր չի պահանջում:

### Մեթոդի հասանելիություն (Method access)

[Method access](#https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods#method-access)

Օբյեկտի վրայից մեթոդի կանչը նման է դաշտին դիմելուն։ Օբյեկտի անունից հետո ավելացվում է կետ, մեթոդի անունը և փակագծեր։ Արգումենտները գրվում են փակագծերում ստորակետերով բաժանված։

```c#
class Motorcycle
{
    private bool isEngineOn = false;
    private int fuel = 0;
    private int mileage = 0;

    // Մեթոդը հասանելի է ցանկացած կոնտեքստում առանց սահմանափակումների
    public void StartEngine()
    {
        if (!isEngineOn)
        {
            isEngineOn = true;
            Console.WriteLine("Engine started.");
        }
        else
        {
            Console.WriteLine("Engine is already running.");
        }
    }

    // Մեթոդը հնարավոր է կանչել միայն տվյալ դասի կամ ածանցյալ դասերում քանի որ այն ունի protected հասանելիության մոդիֆիկատոր
    protected void AddGas(int gallons)
    {
        fuel += gallons;
        Console.WriteLine($"Added {gallons} gallons of gas. Current fuel: {fuel} gallons.");
    }

    // Ածանցյալ դասերում տվյալ մեթոդը կարող է ունենա այլ իրագործում, քանի որ այն ունի virtual մոդիֆիկատորը։ 
    public virtual int Drive(int miles, int speed)
    {
        if (!isEngineOn)
        {
            Console.WriteLine("Cannot drive. The engine is off.");
            return mileage;
        }
        if (fuel <= 0)
        {
            Console.WriteLine("Cannot drive. Out of fuel.");
            return mileage;
        }

        mileage += miles;
        fuel -= miles / 10; // Ենթադրվում է որ 10 մղոնի համար ծախսվում է 1 գալոն
        Console.WriteLine($"Drove {miles} miles at {speed} mph. Total mileage: {mileage} miles. Remaining fuel: {fuel} gallons.");
        return mileage;
    }
}
static void Main()
{
    Motorcycle moto = new Motorcycle();

    moto.StartEngine();
    moto.AddGas(15); // կառաջանա սխալ՝ 'member' is inaccessible due to its protection level
    moto.Drive(5, 20);
    double speed = moto.GetTopSpeed();
    Console.WriteLine($"My top speed is {speed}");
}

```

### Մեթոդի պարամետրեր և արգումենտներ (Method parameters vs. arguments)

[Method parameters vs. arguments](#https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods#method-parameters-vs-arguments)

Մեթոդի սահմանումը ներառում է պահանջվող **պարամետրերի** անուններն ու տեսակները։ Մեթոդը կանչելիս յուրաքանչյուր պարամետրի համար տրամադրվում է կոնկրետ արժեքներ, որոնք կոչվում են **արգումենտներ։** Արգումենտները պետք է համատեղելի լինեն պարամետրի տիպերի հետ։ Կոդում օգտագործված արգումենտի անունները (եթե կան) պարտադիր չէ, որ նույնը լինեն մեթոդում սահմանված պարամետրի անվանումների հետ։

```c#
/*
Այս օրինակում ներկայացված է SomeClass դասը, որը պարունակում է երկու մեթոդներ՝Caller, Square։ Caller մեթոդից կատարվում է Square մեթոդը կանչեր փոխանցելով տարբեր արգումենտներ։
*/

class SomeClass{

    public void Caller()
    {
        int numA = 4;

        // Մեթոդին փոխամցվում է numA փոփոխականի արժեքը
        int productA = Square(numA);

        int numB = 32;
        
        // փոխանվում numB-ն
        int productB = Square(numB);

       // փոխանցվում է ֆիքսված արժեք (literal)
        int productC = Square(12);

        // մեթոդին փոխանցվում է արտահայտություն, որի հաշվարկի արդյունքում ստացված ամբողջ թիվը կհանդիսանա մեթոդի արգումենտ
        productC = Square(productA * 3);
    }

    int Square(int i)
    {
        return input * input;
    }
}
```

### Արժեքների և հղումների փոխանցում (Passing by reference vs. passing by value)

[Passing by reference vs. passing by value](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods#passing-by-reference-vs-passing-by-value)

Արժեքայի տիպերի դեպքում մեթոդին փոխանցվում է նրա պատճենը: Հետևաբար, արգումենտի փոփոխությունները մեթոդում ազդեցություն չունեն սկզբնական օրինակի վրա: Արժեքի տիպի օրինակը հղմամբ փոխանցելու համար անհրաժեշտ է օգտագործել **ref** բանալի բառը:

Ավելի մանրամասն արժեքային և հղում տեսակի տիպերի մասին տես՝ [Արժեքային և Հղում տեսակի տիպեր (Value types, Reference Types)](typesAndVariables.md#արժեքային-և-հղում-տեսակի-տիպեր-value-types-reference-types)

Երբ հղման տիպի օբյեկտ է փոխանցվում մեթոդին՝ փոխանցվում է օբյեկտի հղումը։ Այսինքն՝ մեթոդը ստանում է ոչ թե օբյեկտն ինքնին, այլ օբյեկտի տեղը ցույց տվող արգումենտ։

```c#
    public class SampleRefType
    {
        public int value;
    }

    class Program()
    {
        public static void TestRefType()
        {
            SampleRefType rt = new SampleRefType();
            rt.value = 44; // այս տողով վերագրված արժեքը կփոփոխվի հաջորդ տողով կանչված ModifyObject մեթոդի արդյունքում 
            ModifyObject(rt);
            Console.WriteLine(rt.value); //33
        }

        static void ModifyObject(SampleRefType obj)
        {
            obj.value = 33;
        }

        static void Main()
        {
           TestRefType();
        }
    }
```

Քանի որ օգտագործվում է հղման տեսակ ModifyObject-ում obj պարամետրի արժեքի դաշտում կատարված փոփոխությունը նաև փոխում է rt արգումենտի արժեքի դաշտը TestRefType մեթոդում։ TestRefType մեթոդի դուրս բերվող արժեքը կլինի 33։

### Վերադարձվող արժեքներ

[Return values](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods#return-values)

Մեթոդները կարող են արժեք վերադարձնել կանչողին, եթե վերադարձվող տիպը (մեթոդի անունից առաջ նշված տիպը) **void** չէ։ Մեթոդից արժեք վերադարձնելու համար օգտագործվում է **return** հրամանը։ Հրահանգը, որին հաջորդում է վերադարձվող տեսակին համապատասխանող արժեք, կվերադարձնի այդ արժեքը մեթոդը կանչողին։ Արժեքը կարող է վերադարձվել կանչողին արժեքով կամ հղումով։ Արժեքները կանչողին վերադարձվում են հղումով, եթե մեթոդի ստորագրության (signature) մեջ օգտագործվում է **ref** բանալի բառը և այն հաջորդում է յուրաքանչյուր վերադարձվող բանալի բառին։ Օրինակ, հետևյալ մեթոդի ստորագրությունը և return հրամանը ցույց են տալիս, որ մեթոդը վերադարձնում է հղումով **estDistance** անունով փոփոխականը։

```c#
public ref double GetEstimatedDistance()
{
    return ref estDistance;
}
```

**return** բանալի բառը նաև դադարեցնում է մեթոդի կատարումը։ Եթե վերադարձվող տեսակը void է, ապա արժեք չունեցող **return** հրամանը օգտագործվում է մեթոդի կատարումը դադարեցնելու համար։ Առանց **return** բանալի բառի մեթոդը կդադարեցնի կատարումը, երբ հասնի կոդի բլոկի ավարտին։

```c#
class Program
{
    static void CheckNumber(int number)
    {
        Console.WriteLine("Checking the number...");

        if (number < 0)
        {
            Console.WriteLine("Negative number detected. Exiting method.");
            return; // կավարտվի մեթոդի աշխատանքը
        }

        Console.WriteLine("Number is positive.");
        Console.WriteLine("Processing completed.");
    }

    static void Main()
    {
        Console.WriteLine("Calling CheckNumber with -5:");
        CheckNumber(-5);

        Console.WriteLine("\nCalling CheckNumber with 10:");
        CheckNumber(10);
    }
}

```

Ոչ **void** վերադարձնող տիպ ունեցող մեթոդները պարտադիր պետք է օգտագործեն **return** բանալի բառը՝ արժեք վերադարձնելու համար։

Օրինակ, այս երկու մեթոդներն օգտագործում են  **return** բանալի բառը՝ ամբողջ թվեր վերադարձնելու համար։

```c#
class SimpleMath
{
    public int AddTwoNumbers(int number1, int number2)
    {
        return number1 + number2;
    }

    public int SquareANumber(int number)
    {
        return number * number;
    }
}
```

Մեթոդից վերադարձված արժեքը կարող է օգտագործվել ինքն իրեն, կամ վերագրվել փոփոխականի։

```c#
int result = obj.AddTwoNumbers(1, 2); 
result = obj.SquareANumber(result); // Վերադարձվող արժեքը վերագրվում է փոփոխականի։ 
/* Տվյալ դեպքում result փոփոխականի օգտագործումը պարտադիր չէ Այն կարող է նպաստել կոդի ընթեռնելիությանը, 
կամ կարող է անհրաժեշտ լինել, եթե պետք է պահպանել ստացված արժեքը մեթոդի ամբողջ աշխատանքի ընթացքում։ */

Console.WriteLine(result); // 9

// մեթոդի վերադարձված արժեքն օգտագործվում է ինքն իրեն այլ մեթոդի փոխանցելու համար
result = obj.SquareANumber(obj.AddTwoNumbers(1, 2)); 
Console.WriteLine(result); // 9
```

Մեթոդից հղմամբ վերադարձրած արժեքը օգտագործելու համար դուք պետք է հայտարարեք **ref** լոկալ  փոփոխական, եթե մտադիր եք փոփոխել դրա արժեքը: Օրինակ՝ եթե Planet.GetEstimatedDistance մեթոդը վերադարձնում է Double արժեք հղմամբ, դուք կարող եք այն սահմանել որպես **ref** լոկալ փոփոխական։

```c#
public class Planet
{
    private static double _distance = 4500000d;
    public static ref double GetEstimatedDistance()
    {
        return ref _distance;
    }

}
class Program()
{
    static void Main()
    {

        ref double distance = ref Planet.GetEstimatedDistance();
        distance = 5000000d;
        Console.WriteLine(distance); //5000000

        Console.WriteLine(Planet.GetEstimatedDistance()); //5000000
    }
}

```

Զանգվածի ([array](./collections.md#զանգվածներ)) պարունակությունը փոփոխող մեթոդից անհրաժեշտ չէ վերադարձնել զանգված։ Քանի որ, զանգվածը փոխանցվում է հղումով նրա բովանդակության ցանկացած փոփոխություն դիտարկելի է ցանկացած տեղ։

```c#
static void Main(string[] args)
{
    int[,] matrix = new int[2, 2];
    FillMatrix(matrix);
    // Այժմ matrix-ի բոլոր էլեմենտները հավասար են -1
}

public static void FillMatrix(int[,] matrix)
{
    for (int i = 0; i < matrix.GetLength(0); i++)
    {
        for (int j = 0; j < matrix.GetLength(1); j++)
        {
            matrix[i, j] = -1;
        }
    }
}

```

### Async մեթոդներ

[Async methods](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods#async-methods)

Նշելով մեթոդը async մոդիֆիկատորով, կարող եք օգտագործել await օպերատորը մեթոդում: Երբ կառավարումը հասնում է await արտահայտության async մեթոդում,  մեթոդի կատարումը կանգ է առնում մինչև սպասված առաջադրանքի ավարտը: Երբ առաջադրանքն ավարտվում է, մեթոդի կատարումը շարունակվում է:

Ասինխրոն մեթոդը սովորաբար վերադարձնում է Task<TResult>, Task, IAsyncEnumerable<T> կամ **void** տիպերը: **Void** վերադարձնող ասինխրոն մեթոդը չի կարող սպասվել, և void վերադարձնող մեթոդի կանչողը չի կարող բռնել մեթոդի կողմից նետված բացառությունները: Ասինխրոն մեթոդը կարող է ունենալ ցանկացած առաջադրանքի վերադարձի տեսակ:

Հետևյալ օրինակում **DelayAsync**-ը ասինխրոն մեթոդ է, որն ունի Task<TResult> վերադարձի տեսակ։ **DelayAsync**-ն ունի վերադարձի (return) հրահանգ, որը վերադարձնում է ամբողջ թիվ։ Հետևաբար, **DelayAsync** մեթոդի հայտարարագրումը պետք է ունենա Task<int> վերադարձի տեսակ։ Քանի որ վերադարձի տեսակը Task<int> է, **DoSomethingAsync**-ում **await** արտահայտության կատարման արդյունքում ստացվում է ամբողջ թիվ, ինչպես ցույց է տալիս հետևյալ հրահանգը՝ `int result = await delayTask` :

**Main** մեթոդը ասինխրոն մեթոդի օրինակ է, որն ունի **Task** վերադարձնող տեսակ։ Այն դիմում է **DoSomethingAsync** մեթոդին, և քանի որ այն արտահայտվում է մեկ տողով, կարող ենք բաց թողնել **async** և **await** բանալի բառերը։ Քանի որ **DoSomethingAsync**-ը ասինխրոն մեթոդ է, **DoSomethingAsync**-ի կանչի առաջադրանքը պետք է սպասել, ինչպես ցույց է տալիս հետևյալ հրահանգը՝ `await DoSomethingAsync();` ։

```c#
class Program
{
    static Task Main() => DoSomethingAsync(); // մեկ տողով գրելաձև առանց async, async բանալի բառերի

    /*
    կամ համարժեքը
    static async Task Main()
    {
        await DoSomethingAsync(); 
    }
    */

    static async Task DoSomethingAsync()
    {
        Task<int> delayTask = DelayAsync();
        int result = await delayTask;

        // Նախորդող երկու տողերը կարող են միավորվել հետևյալ արտահատությամբ
        //int result = await DelayAsync();

        Console.WriteLine($"Result: {result}");
    }

    static async Task<int> DelayAsync()
    {
        await Task.Delay(100);
        return 5;
    }
}
```

## Հասանելիության մոդիֆիկատորներ (Access Modifiers)

Բոլոր տիպերը և տիպի անդամները ունեն հասանելիության մակարդակ։ Հասանելիության մակարդակը որոշում է, թե արդյոք դրանք կարող են օգտագործվել այլ տեղ կոդում. նույն, կամ այլ **assembly** -ներում։ **assembly -ն** .dll կամ .exe ֆայլ է, որը ստեղծվում է մեկ կամ մի քանի .cs ֆայլերի հիման վրա մեկ կոմպիլյացիայի միջոցով։

Օգտագործեք հետևյալ հասանելիության մոդիֆիկատորները՝ տիպի կամ անդամի հայտարարության ժամանակ, հասանելիությունը նշելու համար։

Այսպիսով տիպի կամ անդամի հետևյալ հասանելիության մոդիֆիկատորների դեպքում այն հասանելի է՝

- public: Ցանկացած տեղ, ցանկացած assembly-ի կոդից։
- private: Միայն նույն դասում։
- protected: Միայն նույն կամ [ածանցյալ դասում](./inheritance.md#ժառանգում-inheritance)։
- internal: Միայն նույն assembly-ում։
- protected internal: Միայն նույն assembly-ում կամ մեկ այլ assembly-ի ածանցյալ դասում։
- private protected: Միայն նույն assembly-ի և նույն դասի կամ ածանցյալ դասում։
- file: Միայն նույն ֆայլում։
  
[Access Modifiers](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/access-modifiers)
