# Կոլեկցիաներ և զանգվածներ

## Բովանդակություն

- [Կոլեկցիաներ և զանգվածներ](#կոլեկցիաներ-և-զանգվածներ)
  - [Բովանդակություն](#բովանդակություն)
  - [Ինդեքսավորվող կոլեկցիաներ(Indexable collections)](#ինդեքսավորվող-կոլեկցիաներindexable-collections)
  - [Key/value pair collections](#keyvalue-pair-collections)
  - [Զանգվածներ](#զանգվածներ)
    - [Միաչափ զանգված](#միաչափ-զանգված)
      - [Միաչափ զանգվածների փոխանցում որպես արգումենտներ](#միաչափ-զանգվածների-փոխանցում-որպես-արգումենտներ)
    - [Բազմաչափ զանգվածներ (Multidimensional arrays)](#բազմաչափ-զանգվածներ-multidimensional-arrays)
      - [Բազմաչափ զանգվածների փոխանցում որպես արգումենտներ](#բազմաչափ-զանգվածների-փոխանցում-որպես-արգումենտներ)
    - [Անկանոն զանգվածներ (Jagged arrays)](#անկանոն-զանգվածներ-jagged-arrays)
    - [Անուղղակիորեն տիպիզացված զանգվածներ (Implicitly typed arrays)](#անուղղակիորեն-տիպիզացված-զանգվածներ-implicitly-typed-arrays)

Կոլեկցիաները ապահովում են օբյեկտների խմբերի հետ աշխատելու ճկուն միջոց: Կոլեկցիաները hնարավոր է դասակարգել հետևյալ բնութագրերով.

- **Տարրերի հասանելիություն** Յուրաքանչյուր հավաքածու կարող է թվարկվել՝ յուրաքանչյուր տարրին հասանելիություն ունենալու համար հերթականությամբ: Որոշ հավաքածուներում տարրերին հասանելիությունը կատարվում է ինդեքսով, որը տարրի դիրքն է կոլեցկցիայում: Ամենատարածված օրինակը System.Collections.Generic.List<T>-ն է: Այլ տեսակի կոլեկցիաների դեպքում տարրերին հասանելիությունը իրականացվում է բանալիով, որտեղ արժեքը կապված է մեկ բանալիի հետ: Նշված տեսակի ամենատարածված օրինակը System.Collections.Generic.Dictionary<TKey,TValue>-ն է: Դուք կարող եք ընտրել այս հավաքածուների տեսակների միջև՝ հիմնվելով այն բանի վրա, թե ինչպես պետք է հասանելիություն ունենաք տարրերին:
- **Արդյունավետության պրոֆիլ**  Յուրաքանչյուր հավաքածու ունի տարբեր արդյունավետության պրոֆիլներ այնպիսի գործողությունների համար, ինչպիսիք են տարր ավելացնելը, տարր գտնելը կամ տարր հեռացնելը: Դուք կարող եք ընտրել կոլեկցիայի տեսակ՝ հիմնվելով ամենաշատ օգտագործվող գործողությունների վրա:
- **Դինամիկ աճ և փոքրացում**  Կոլեկցիաների մեծ մասը թույլատրում է տարրերի դինամիկ ավելացմանը կամ հեռացմանը: Array, System.Span<T> և System.Memory<T>-ն չեն թույլատրում:

## Ինդեքսավորվող կոլեկցիաներ(Indexable collections)

[Indexable collections](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/collections#indexable-collections)

Ինդեքսավորվող է այն կոլեկցիան է, որտեղ հնարավոր է հասանելիություն ստանալ տարրի օգտագործելով նրա ինդեքսը։ Ինդեքսը հաջորդականության մեջ դրանից առաջ գտնվող տարրերի քանակն է։ Հետևաբար, 0 ինդեքսով տարրի հղումը առաջին տարրն է, 1 ինդեքսով՝ երկրորդը և այլն։ Այս օրինակներում օգտագործվում է List<T> դասը։ Սա ամենատարածված ինդեքսավորվող կոլեկցիան է։ Հետևյալ օրինակում ստեղծում և ինիցիալիզացվում է տողերի ցանկ, հեռացվում և ավելացնում է տարր ցանկի վերջում։

```c#
// Ստեղծվում և ինիցիալիզացվում է string-երի ցուցակ (list)
List<string> salmons = ["chinook", "coho", "pink", "sockeye"];

// Ցիկլի միջոցով անցնում ենք ցուցակի էլեմենտների վրայով տպելով յուրաքանչյուրը
foreach (var salmon in salmons)
{
    Console.Write(salmon + " ");
}
// Output: chinook coho pink sockeye

// Հեռացնում ենք ելեմենտ 
salmons.Remove("coho");


// Ցիկլի միջոցով անցնում ենք էլեմենտների վրայով օգտագործելով ինդեքսը
for (var index = 0; index < salmons.Count; index++) // salmons.Count -ի արժեքը ցուցակում առկա էլեմենտների քանակն է
{
    Console.Write(salmons[index] + " ");
}
// Output: chinook pink sockeye

// Ավելացվում է հեռացված տողը
salmons.Add("coho");
 
foreach (var salmon in salmons)
{
    // Output: chinook pink sockeye coho // Add մեթոդի միջոցով ավելացված էլեմենտները ավելացվում են ցուցակի վերջում
    Console.Write(salmon + " ");
}
```

Հետևյալ օրինակում տարրերը ցանկից հեռացնում են ինդեքսով։ foreach հրամանի փոխարեն օգտագործվում է for հրամանը հակառակ հեթականությամբ իտերացնելու համար։ RemoveAt մեթոդի աշխատանքից հետո հեռացված տարրից հետո գտնվող տարրերն ստանում են ավելի փոքր ինդեքսի արժեք։

```c#
List<int> numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

// Հեռացվում են կենտ թվերը
for (var index = numbers.Count - 1; index >= 0; index--)
{
    if (numbers[index] % 2 == 1)
    {
        // Հեռացվում է սահմանված ինդեքսով էլէեմնտը
        numbers.RemoveAt(index);
    }
}

// Կանչվում է ցուցակի ForEach մեթոդը, որին փոխանցվում է lambda արտահայտություն։
// ForEach -ը list -ի մեթոդ է, որին հնարավոր է փոխանցել լոկալ ֆունկցիա կամ lambda արտահայտություն, որը 
// այնուհետև կկանչվի  ցուցակի յուրաքանչյուր էլեմենտի համար։ Ամեն անգամ այն կանչելիս նրան կփոխանցվի ցուցակի 
// հեթական էլեմենտը
numbers.ForEach(
    number => Console.Write(number + " "));
// Output: 0 2 4 6 8

```

Ցուցակների մեթոդների ամբողջական ցանկին կարող եք ծանոթանալ հետևյալ հումով՝
[List<T> Class](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1?view=net-9.0)

## Key/value pair collections

[Key/value pair collections](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/collections#keyvalue-pair-collections)

Այս օրինակներում օգտագործվում է Dictionary<TKey,TValue> դասը։ Սա ամենատարածված բառարանային կոլեկցիան է։ Բառարանային կոլեկցիան թույլ է տալիս հասանելիություն ապահովվել իր տարրերին՝ օգտագործելով յուրաքանչյուր տարրի բանալին։ Բառարանի յուրաքանչյուր ավելացում բաղկացած է արժեքից և դրան կից բանալիից։

```c#
private static void IterateThruDictionary()
{
    // վերագրում ենք BuildDictionary մեթոդի կողմից վերադարձրած բառարանը elements փոփոխականին
    Dictionary<string, Element> elements = BuildDictionary();

    // Ցիկլի ամեն պտույտի (iteration) ժամանակ kvp պարամետրին կվերագրվի բառարանի հեթական բանալի-արժեք զույգը։
    foreach (KeyValuePair<string, Element> kvp in elements)
    {
        // վերագրվում է հեթական արժեքը theElement փոփոխականին
        Element theElement = kvp.Value;


        Console.WriteLine("key: " + kvp.Key); // դուրս է բերվում "key: " տողը և հեթական բանալու արժեքը
        
        //դուրս է բերվում "values: " տողը և հերթական արժեքի՝ Symbol, Name, AtomicNumber հատկություններն
        Console.WriteLine("values: " + theElement.Symbol + " " +
            theElement.Name + " " + theElement.AtomicNumber);
    }
}

public class Element
{
    public required string Symbol { get; init; }
    public required string Name { get; init; }
    public required int AtomicNumber { get; init; }
}

// Տվյալ մեթոդը վերադարձնում է բառարան (dictionary), որը կարող է ունենալ string տեսակի բանալներ (keys) և 
// Element տիպի արժեքներ (values)։
// քանի որ հայտնի է մեթոդի վերադարձվող տիպը օգտագործվել է կրճատ գրելաձև`
//           new () {...}
// որը համարժեք է`
//           new Dictionary<string, Element> 
//  Նույն կրճատ գրելաձևն օգտագործվել է արժեքները սահմանելիս`
//           new (){ Symbol="K", Name="Potassium", AtomicNumber=19}
// որը համարժեք է`
//           new Element{ Symbol="K", Name="Potassium", AtomicNumber=19}}, 
// սա հնարավոր է քանի որ մեթոդի ստորագրության մեջ ֆիքսված է, որ վերադարձվող բառարանի արժեքները պետք է լինեն
// Example տիպի։

private static Dictionary<string, Element> BuildDictionary() =>
    new () 
    {
        {"K",
            new (){ Symbol="K", Name="Potassium", AtomicNumber=19}},
        {"Ca",
            new (){ Symbol="Ca", Name="Calcium", AtomicNumber=20}},
        {"Sc",
            new (){ Symbol="Sc", Name="Scandium", AtomicNumber=21}},
        {"Ti",
            new (){ Symbol="Ti", Name="Titanium", AtomicNumber=22}}
    };

```

Հետևյալ օրինակում օգտագործվում են `ContainsKey` մեթոդը և Dictionary-ի `Item[]` հատկությունը՝ տարրը բանալիով արագ գտնելու համար: `Item` հատկությունը թույլ է տալիս հասանելիություն ստանալ տարրերին օգտագործելով C#-ի elements[symbol]-ը:

```c#
//Բանալու առկայության ստուգումը իրականցնվում է քանի որ նրա բացակայության դեպքում կառաջանա սխալ(KeyNotFoundException)
if (elements.ContainsKey(symbol) == false)  
{
    Console.WriteLine(symbol + " not found");
}
else
{
    Element theElement = elements[symbol]; // ստանում ենք տարրը
    Console.WriteLine("found: " + theElement.Name);
}

```

Հետևյալ օրինակը փոխարենը օգտագործում է `TryGetValue` մեթոդը՝ տարրը բանալիով արագ գտնելու համար։

```c#
if (elements.TryGetValue(symbol, out Element? theElement) == false)
    Console.WriteLine(symbol + " not found");
else
    Console.WriteLine("found: " + theElement.Name);
```

**elements**-ը `Dictionary<string, Element`> տիպի փոփոխական է։

**TryGetValue** մեթոդը փորձում է գտնել symbol անունով բանալին բառարանում։

Այն վերադարձնում է․

- true՝ եթե բանալին գտնվել է։
- false՝ եթե բանալին չի գտնվել։

Եթե բանալին գտնվել է, ապա **theElement** փոփոխականին կվերագրվի համապատասխան արժեքը (Element տիպի)։

Եթե բանալին չի գտնվել, ապա **theElement**-ը կստանա null արժեքը (այդ պատճառով այն հայտարարվում է որպես nullable Element? տիպով)։

Բառարանների մեթոդների ամբողջական ցանկին կարող եք ծանոթանալ այս հումով՝ [Dictionary<TKey,TValue>](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=net-9.0#methods)

## Զանգվածներ

Զանգվածում հնարավոր է պահել նույն տիպի մի քանի փոփոխականներ։ Զանգվածը հայտարարելիս նշվում է նրա տարրերի տեսակը։ Եթե ցանկանում եք, որ զանգվածը պահպանի ցանկացած տիպի տարրեր, կարող եք որպես դրա տեսակ նշել օբյեկտը։ C#-ի միասնական տիպային համակարգում բոլոր տեսակները՝ նախապես սահմանված և օգտատիրոջ կողմից սահմանված, հղման տեսակներն ու արժեքի տեսակները, ժառանգում են ուղղակիորեն կամ անուղղակիորեն օբյեկտից։

```c#
type[] arrayName;
```

Զանգվածը հղման տեսակ է, ուստի այն կարող է լինել **nullable** հղման տեսակ։ Տարրերի տեսակները կարող են լինել հղման տեսակներ, ուստի զանգվածը կարող է հայտարարվել nullable հղման տեսակներ պահելու համար։ Հետևյալ օրինակները ցույց են տալիս զանգվածի կամ տարրերի nullable - ությունը հայտարարելու համար օգտագործվող տարբեր շարահյուսություն։

```c#
type?[] arrayName; // nullable տարրերի տեսակների ոչ nullable զանգված։
type[]? arrayName; // nullable զանգված ոչ nullable էլեմենտների տիպերով։
type?[]? arrayName; // nullable զանգված nullable էլեմենտների տիպերով։
```

Առանց ինիցիալիզացնելու բոլոր էլէմենտները ունեն իրենց լռելյայն արժեքը

```c#
int[] numbers = new int[10]; // Բոլոր էլեմենտները ունեն 0 արժեք։
string[] messages = new string[10]; // Բոլոր էլեմենտները null եմ։
```

**Զանգվածներն ունեն հետևյալ առանձնահատկությունները**

- Զանգվածները կարող են լինել միաչափ, բազմաչափ կամ Անկանոն (jagged)։
- Զանգվածի չափսերը սահմանվում են փոփոխականի հայտարարման պահին։ Յուրաքանչյուր չափման երկարությունը սահմանվում է զանգվածի օրինակն ստեղծելիս և չի կարող փոխվել դրա կյանքի ընթացքում։
- Անկանոն (jagged) զանգվածը զանգվածների զանգված է, և յուրաքանչյուր ներքին զանգված ունի null որպես լռելյայն արժեք։
- Զանգվածները զրոյից են ինդեքսավորվում․ n տարր ունեցող զանգվածն ինդեքսավորվում է 0-ից մինչև n-1։
- Զանգվածի տարրերը կարող են լինել ցանկացած տիպի, այդ թվում՝ զանգված տիպի։
- Զանգվածային տիպերը հղման տիպեր են, որոնք ժառանգված են աբստրակտ Array բազային տիպից։ Բոլոր զանգվածները իրականացնում են IList և IEnumerable ինտերֆեյսները։ Կարող եք օգտագործել foreach ցիկլը՝ զանգվածի տարրերով անցնելու համար։ Միաչափ զանգվածները նաև իրականացնում են IList<T> և IEnumerable<T>։

Զանգվածի տարրերը կարող են նախապես տրվել ստեղծման պահին։ C# 12-ից սկսած՝ կարելի է օգտագործել Collection արտահայտություններ ([ ]) զանգվածները ինիցիալիզացնելու համար։ Չինիցիալիզացված տարրերը ստանում են լռելյայն արժեք։ Հղման տիպերը ստանում են null, իսկ արժեքային տիպերը՝ 0։

```c#
// Հայտարարվում է 5 ամբողջ թվերից բաղկացած միաչափ զանգված։
int[] array1 = new int[5];

// Հայտարարվում և սահմանվում են զանգվածը էլեմենտներով։ 
int[] array2 = [1, 2, 3, 4, 5, 6];

// Հայտարարվում է երկչափանի զանգված։
int[,] multiDimensionalArray1 = new int[2, 3];

// Հայտարարվում և սահմանվում է երկչափանի զանգված էլեմենտներով։
int[,] multiDimensionalArray2 = { { 1, 2, 3 }, { 4, 5, 6 } };

// Հայտարարվում է jagged զանգված
int[][] jaggedArray = new int[6][];

// Սահմանվում է նախորդ քայլով հայտարարված առաջին էլեմենտի արժեքը
jaggedArray[0] = [1, 2, 3, 4];

```

Զանգվածները ինիցիալիզացնելիս հնարավոր է օգտագործել հետևյալ գրելաձևերը՝

```c#
// Collection expressions:
int[] array = [1, 2, 3, 4, 5, 6]; // Հասանելի է C# 12 տարբերակից
// Alternative syntax:
int[] array2 = {1, 2, 3, 4, 5, 6};
```

### Միաչափ զանգված

Միաչափ զանգվածը նման տարրերի հաջորդականություն է: Տարրին հասանելությունը իրականացվում է ինդեքսի միջոցով: Ինդեքսը նրա կարգային դիրքն է հաջորդականության մեջ: Զանգվածի առաջին տարրը գտնվում է 0 ինդեքսում: Հնարավոր է ստեղծել միաչափ զանգված՝ օգտագործելով new օպերատորը, որը նշում է զանգվածի տարրի տեսակը և տարրերի քանակը: 

```c#
// Հայտարարվում է հինգ ամբողջ թվերից բաղկացած չինիցիալիզացված զանգված՝ array[0]-ից մինչև array[4]: Զանգվածի տարրերը ինիցիալիզացվում են են տարրի տեսակի լռելյայն արժեքով, որը 0 է ամբողջ թվերի համար:
int[] array = new int[5];

//Հայտարարում է տողերի զանգված և ինիցիալիզացվում են այդ զանգվածի բոլոր յոթ արժեքները:
string[] weekDays = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];

Console.WriteLine(weekDays[0]);
Console.WriteLine(weekDays[1]);
Console.WriteLine(weekDays[2]);
Console.WriteLine(weekDays[3]);
Console.WriteLine(weekDays[4]);
Console.WriteLine(weekDays[5]);
Console.WriteLine(weekDays[6]);

/* Դուրս բերվող արժեքներ:
Sun
Mon
Tue
Wed
Thu
Fri
Sat
*/
```

#### Միաչափ զանգվածների փոխանցում որպես արգումենտներ

Հնարավոր է մեթոդին փոխանցել ինիցիալիզացված միաչափ զանգված։ Հետևյալ օրինակում տողերի զանգվածը ինիցիալիզացվում և փոխանցվում է որպես արգումենտ DisplayArray մեթոդին։ Մեթոդը ցուցադրում է զանգվածի տարրերը։ Հաջորդը, ChangeArray մեթոդը շրջում է զանգվածի տարրերը, ապա ChangeArrayElements մեթոդը փոփոխում է զանգվածի առաջին երեք տարրերը։ Յուրաքանչյուր մեթոդ վերադարձնելուց հետո DisplayArray մեթոդը ցույց է տալիս, որ զանգվածի արժեքով փոխանցումը չի կանխում զանգվածի տարրերի փոփոխությունները։

```c#
class ArrayExample
{
    static void DisplayArray(string[] arr) => Console.WriteLine(string.Join(" ", arr));

    // Փոփոխում է զանգվածը շրջելով էլեմենտները
    static void ChangeArray(string[] arr) => Array.Reverse(arr);

    static void ChangeArrayElements(string[] arr)
    {
        // Փոփոխում է զանգվածի առաջին երեք էլեմենտների արեժքները
        arr[0] = "Mon";
        arr[1] = "Wed";
        arr[2] = "Fri";
    }

    static void Main()
    {
        // Հայտարարվում և ինիցիալիզացվում է զանգված
        string[] weekDays = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
        // Ցուցադրվում է զանգվածի էլեմենտները
        DisplayArray(weekDays);
        Console.WriteLine();

        // Շրջում է զանգվածի էլեմենտները
        ChangeArray(weekDays);
        // Կրկին ցույց է տալիս զանգվածը ստուգելու համար որ էլեմենտները մնացել են շրջված
        Console.WriteLine("Array weekDays after the call to ChangeArray:");
        DisplayArray(weekDays);
        Console.WriteLine();

        // Արժեքներ են վերագրում է զանգվածի էլեմենտներին
        ChangeArrayElements(weekDays);
        // Կրկին ցույց է տրվում զանգվածը համոզվելու համար որ այն փոփոխվել է
        Console.WriteLine("Array weekDays after the call to ChangeArrayElements:");
        DisplayArray(weekDays);
    }
}
// Աշխատանքի ընթացքում դուրս բերվող արժեքներն են:
//        Sun Mon Tue Wed Thu Fri Sat
//
//        ChangeArray կանչելուց հետո
//        Sat Fri Thu Wed Tue Mon Sun
//
//        ChangeArrayElements կանչելուց հետո
//        Mon Wed Fri Wed Tue Mon Sun

```

### Բազմաչափ զանգվածներ (Multidimensional arrays)

Զանգվածները կարող են ունենալ մեկից ավելի չափումներ: Օրինակ, հետևյալ օրինակում ստեղծում է չորս զանգված: Երկու զանգվածները ունեն երկու չափումներ: Երկու զանգված ունեն երեք չափումներ: Առաջին երկու դեպքերում հայտարարվում է յուրաքանչյուր չափման երկարությունը, բայց չեն ինիցիալիզացվում զանգվածի արժեքները: Երկրորդ երկու հայտարարությունները օգտագործում են ինիցիալիզատոր՝ բազմաչափ զանգվածում յուրաքանչյուր տարրի արժեքները սահմանելու համար:

```c#
int[,] array2DDeclaration = new int[4, 2];

int[,,] array3DDeclaration = new int[4, 2, 3];

// Երկչափանի զանգված
int[,] array2DInitialization =  { { 1, 2 }, { 3, 4 }, { 5, 6 }, { 7, 8 } };
// Եռաչափ զանգված
int[,,] array3D = new int[,,] { { { 1, 2, 3 }, { 4,   5,  6 } },
                                { { 7, 8, 9 }, { 10, 11, 12 } } };

// Հասանելիություն զանգվածի էլեմենտներին
System.Console.WriteLine(array2DInitialization[0, 0]);
System.Console.WriteLine(array2DInitialization[0, 1]);
System.Console.WriteLine(array2DInitialization[1, 0]);
System.Console.WriteLine(array2DInitialization[1, 1]);

System.Console.WriteLine(array2DInitialization[3, 0]);
System.Console.WriteLine(array2DInitialization[3, 1]);
// Դուրս բերվող տողեր:
// 1
// 2
// 3
// 4
// 7
// 8

System.Console.WriteLine(array3D[1, 0, 1]);
System.Console.WriteLine(array3D[1, 1, 2]);
// Դուրս բերվող տողեր:
// 8
// 12

// Ստանում ենք տրված չափողականության տարրերի ընդհանուր քանակը կամ երկարությունը։
var allLength = array3D.Length;
var total = 1;
for (int i = 0; i < array3D.Rank; i++)
{
    total *= array3D.GetLength(i);
}
System.Console.WriteLine($"{allLength} equals {total}");
// Դուրս բերվող տողեր:
// 12 equals 12

```

Բազմաչափ զանգվածների համար տարրերը հատվում են այնպես, որ սկզբում ամենաաջ չափման ինդեքսները մեծանում են, ապա հաջորդ ձախ չափմանը և այլն, մինչև ամենաձախ ինդեքսը։ Հետևյալ օրինակը թվարկում է և՛ 2D, և՛ 3D զանգվածները։

```c#
int[,] numbers2D = { { 9, 99 }, { 3, 33 }, { 5, 55 } };

foreach (int i in numbers2D)
{
    System.Console.Write($"{i} ");
}
// Դուրս բերվող արժեքներ՝ 9 99 3 33 5 55

int[,,] array3D = new int[,,] { { { 1, 2, 3 }, { 4,   5,  6 } },
                        { { 7, 8, 9 }, { 10, 11, 12 } } };
foreach (int i in array3D)
{
    System.Console.Write($"{i} ");
}
// Դուրս բերվող արժեքներ՝ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12

```

Երկչափ զանգվածում կարող եք ձախ ինդեքսը պատկերացնել որպես տող, իսկ աջ ինդեքսը՝ որպես սյուն։ Այնուամենայնիվ, բազմաչափ զանգվածների դեպքում, ներդրված for ցիկլի օգտագործումը ձեզ ավելի մեծ վերահսկողություն է տալիս զանգվածի տարրերի մշակման հերթականության նկատմամբ։

```c#
int[,,] array3D = new int[,,] { 
        { 
            { 1, 2, 3 }, { 4,   5,  6 } 
        },
        {
            { 7, 8, 9 }, { 10, 11, 12 } 
        } 
    };

for (int i = 0; i < array3D.GetLength(0); i++)
{
    for (int j = 0; j < array3D.GetLength(1); j++)
    {
        for (int k = 0; k < array3D.GetLength(2); k++)
        {
            System.Console.Write($"{array3D[i, j, k]} ");
        }
        System.Console.WriteLine();
    }
    System.Console.WriteLine();
}
// Դուրս բերվող տողեր (ներառյալ դատարկ տողերը):
// 1 2 3
// 4 5 6
//
// 7 8 9
// 10 11 12
//

```

#### Բազմաչափ զանգվածների փոխանցում որպես արգումենտներ

Ինիցիալիզացված բազմաչափ զանգվածը մեթոդին փոխանցում եք նույն ձևով, ինչպես միաչափ զանգվածը։ Հետևյալ կոդը ցույց է տալիս print մեթոդի մասնակի (partial) հայտարարումը, որն ընդունում է երկչափ զանգված որպես իր արգումենտ։ Հնարավոր է և նոր զանգված փոխանցել մեկ քայլով, ինչպես ցույց է տրված հետևյալ օրինակում։ Հետևյալ օրինակում ամբողջ թվերի երկչափ զանգվածը նախնականացվում է և փոխանցվում Print2DArray մեթոդին։ Մեթոդը ցուցադրում է զանգվածի տարրերը։

```c#
static void Print2DArray(int[,] arr)
{
    // Display the array elements.
    for (int i = 0; i < arr.GetLength(0); i++)
    {
        for (int j = 0; j < arr.GetLength(1); j++)
        {
            System.Console.WriteLine($"Element({i},{j})={arr[i,j]}");
        }
    }
}
static void ExampleUsage()
{
    // Փոխանցվում է զանգվածը որպես արգումենտ
    Print2DArray(new int[,] { { 1, 2 }, { 3, 4 }, { 5, 6 }, { 7, 8 } });
}
/* Դուրս բերվող տողեր:
    Element(0,0)=1
    Element(0,1)=2
    Element(1,0)=3
    Element(1,1)=4
    Element(2,0)=5
    Element(2,1)=6
    Element(3,0)=7
    Element(3,1)=8
*/
```

### Անկանոն զանգվածներ (Jagged arrays)

Անկանոն  զանգվածը զանգված է, որի տարրերը նույնպես զանգվածներ են, հնարավոր է՝ տարբեր չափերի: Անկանոն զանգվածը երբեմն անվանում են «զանգվածների զանգված»: Դրա տարրերը հղման տեսակներ են և ինիցիալիզացվում են null արժեքով: Հետևյալ օրինակները ցույց են տալիս, թե ինչպես հայտարարել, ինիցիալիզացնել և հասանելիություն ստանալ անկանոն զանգվածների: Առաջին օրինակը՝ jaggedArray-ը, հայտարարվում է մեկ հրահանգում: Յուրաքանչյուր պարունակվող զանգված ստեղծվում է հաջորդող հրահանգներում: Երկրորդ օրինակը՝ jaggedArray2-ը, հայտարարվում և ինիցիալիզացվում է մեկ հրահանգում: Հնարավոր է խառնել անկանոն և բազմաչափ զանգվածները: Վերջին օրինակը՝ jaggedArray3-ը, միաչափ անկանոն զանգվածի հայտարարում և նախնականացում է, որը պարունակում է տարբեր չափերի երեք երկչափ զանգվածի տարրեր:

```c#
int[][] jaggedArray = new int[3][];

jaggedArray[0] = [1, 3, 5, 7, 9];
jaggedArray[1] = [0, 2, 4, 6];
jaggedArray[2] = [11, 22];

int[][] jaggedArray2 =
[
    [1, 3, 5, 7, 9],
    [0, 2, 4, 6],
    [11, 22]
];

// Վերագրվում է 77 առաջին զանգվածի երկրորդ էլեմենտին ([1]) 
jaggedArray2[0][1] = 77;

// Վերագրվում է 88 երրորդ զանգվածի ([2]) երկրորդ էլեմենտին ([1])
jaggedArray2[2][1] = 88;

int[][,] jaggedArray3 =
[
    new int[,] { {1,3}, {5,7} },
    new int[,] { {0,2}, {4,6}, {8,10} },
    new int[,] { {11,22}, {99,88}, {0,9} }
];

Console.Write("{0}", jaggedArray3[0][1, 0]);
Console.WriteLine(jaggedArray3.Length);

```

### Անուղղակիորեն տիպիզացված զանգվածներ (Implicitly typed arrays)

Հնարավոր է ստեղծել անուղղակիորեն տիպավորված զանգված, որտեղ զանգվածի օրինակի տեսակը որոշվում է զանգվածի նախնականացուցիչում նշված տարրերից: Անուղղակիորեն տիպավորված ցանկացած փոփոխականի կանոնները վերաբերում են նաև անուղղակիորեն տիպավորված զանգվածներին: Լրացուցիչ տեղեկությունների համար տե՛ս Անուղղակիորեն տիպավորված տեղական փոփոխականներ բաժինը:

Հետևյալ օրինակները ցույց են տալիս, թե ինչպես ստեղծել անուղղակիորեն տիպիզացված զանգված.

```c#
int[] a = new[] { 1, 10, 100, 1000 }; // int[]

// Հասանելիություն զանգվածին
Console.WriteLine("First element: " + a[0]);
Console.WriteLine("Second element: " + a[1]);
Console.WriteLine("Third element: " + a[2]);
Console.WriteLine("Fourth element: " + a[3]);

/* Դուրս բերվող արժեքներ
First element: 1
Second element: 10
Third element: 100
Fourth element: 1000
*/

var b = new[] { "hello", null, "world" }; // string[]

// Accessing elements of an array using 'string.Join' method
// Հասանելիություն զանգվածի էլեմենտներին օգտգործելով 'string.Join' մեթոդը
Console.WriteLine(string.Join(" ", b));

/* Դուրս բերվող արժեք
hello  world
*/

// Միաչափ անկանոն (jagged) զանգված
int[][] c =
[
    [1,2,3,4],
    [5,6,7,8]
];
// Ցիկլով անցում արտաքին զանգվածով
for (int k = 0; k < c.Length; k++)
{
    // Անցում ներքին զանգվածով
    for (int j = 0; j < c[k].Length; j++)
    {
        // Տպվում է յուրաքանչյուր էլեմենտը
        Console.WriteLine($"Element at c[{k}][{j}] is: {c[k][j]}");
    }
}
/* Դուրս բերվող արժեքներ
Element at c[0][0] is: 1
Element at c[0][1] is: 2
Element at c[0][2] is: 3
Element at c[0][3] is: 4
Element at c[1][0] is: 5
Element at c[1][1] is: 6
Element at c[1][2] is: 7
Element at c[1][3] is: 8
*/

// տողերի անկանոն զանգված
string[][] d =
[
    ["Luca", "Mads", "Luke", "Dinesh"],
    ["Karen", "Suma", "Frances"]
];

// Ցիկլով անցում արտաքին զանգվածով
int i = 0;
foreach (var subArray in d)
{
    // Անցում ներքին զանգվածով
    int j = 0;
    foreach (var element in subArray)
    {
        // Տպվում է յուրաքանչյուր էլեմենտը
        Console.WriteLine($"Element at d[{i}][{j}] is: {element}");
        j++;
    }
    i++;
}
/* Դուրս բերվող արժեքներ

Element at d[0][0] is: Luca
Element at d[0][1] is: Mads
Element at d[0][2] is: Luke
Element at d[0][3] is: Dinesh
Element at d[1][0] is: Karen
Element at d[1][1] is: Suma
Element at d[1][2] is: Frances
*/
```

Նախորդ օրինակում անուղղակիորեն տիպիզացված զանգվածների դեպքում ինիցիալիզացիայի հրահանգի ձախ կողմում չեն օգտագործվել քառակուսի փակագծեր։ Բացի այդ, անկանոն զանգվածները ինիցիալիզացվել են new []-ի միջոցով, ինչպես միաչափ զանգվածները։

Զանգված պարունակող անանուն տիպ (anonymous) ստեղծելիս, զանգվածը պետք է անուղղակիորեն տիպիզացված լինի օբյեկտի ինիցիալիզատորում: Հետևյալ օրինակում contacts-ը անուղղակիորեն անանուն տիպերի տիպիզացված զանգված է, որոնցից յուրաքանչյուրը պարունակում է PhoneNumbers անունով զանգված: Var բանալի բառը չի օգտագործվում օբյեկտի նախնականացուցիչների ներսում։

```c#
var contacts = new[]
{
    new
    {
        Name = "Eugene Zabokritski",
        PhoneNumbers = new[] { "206-555-0108", "425-555-0001" }
    },
    new
    {
        Name = "Hanying Feng",
        PhoneNumbers = new[] { "650-555-0199" }
    }
};
```
