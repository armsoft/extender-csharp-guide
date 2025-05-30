# LINQ հարցումներ

## Բովանդակություն

- [LINQ հարցումներ](#linq-հարցումներ)
  - [Բովանդակություն](#բովանդակություն)
  - [Ներածություն](#ներածություն)
  - [LINQ հարցումներ գրեկու ձեռնարկ](#linq-հարցումներ-գրեկու-ձեռնարկ)
    - [Հիշողության մեջ տվյալների աղբյուրի ստեղծում](#հիշողության-մեջ-տվյալների-աղբյուրի-ստեղծում)
    - [Հարցման ստեղծում](#հարցման-ստեղծում)
    - [Հարցման կատարում](#հարցման-կատարում)
    - [Հարցման արդյունքների դասավորում](#հարցման-արդյունքների-դասավորում)
    - [Արդյունքների խմբավորում](#արդյունքների-խմբավորում)
    - [Դասավորում ըստ բանալու և արժեքի](#դասավորում-ըստ-բանալու-և-արժեքի)
    - [Մեթոդի շարահյուսության օգտագործում հարցման արտահայտության մեջ](#մեթոդի-շարահյուսության-օգտագործում-հարցման-արտահայտության-մեջ)
    - [Փոխակերպում կամ արտապատկերում select արտահայտության մեջ](#փոխակերպում-կամ-արտապատկերում-select-արտահայտության-մեջ)

## Ներածություն

Հարցումը արտահայտություն է, որի միջոցով տվյալներ են ստանում տվյալների աղբյուրից: Տարբեր տվյալների աղբյուրներ ունեն տարբեր հարցման լեզուներ, օրինակ՝ SQL-ը՝ ռելացիոն տվյալների բազաների համար է և XQuery-ն՝ XML-ի համար:
Յուրաքանչյուր տվյալների աղբյուրի կամ ձևաչափի հետ աշխատելու համար անհրաժեշտություն է առաջանում սովորել հաապատասխան հարցման լեզուն։
LINQ-ն պարզեցնում է այս իրավիճակը՝ առաջարկելով հետևողական C# լեզվի մոդել տվյալների աղբյուրների և ձևաչափերի տեսակների համար: LINQ հարցման մեջ դուք միշտ աշխատում եք C# օբյեկտների հետ: Դուք օգտագործում եք նույն հիմնական կոդավորման ձևանմուշները՝ XML փաստաթղթերում, SQL տվյալների բազաներում, .NET հավաքածուներում և ցանկացած այլ ձևաչափում տվյալների հարցման և փոխակերպման համար:

## LINQ հարցումներ գրեկու ձեռնարկ

[Tutorial: Write queries in C# using language integrated query (LINQ)](https://learn.microsoft.com/en-us/dotnet/csharp/linq/get-started/walkthrough-writing-queries-linq)

Այս ձեռնարկում կստեղծենք տվյալների աղբյուր և կգրեք մի քանի LINQ հարցումներ: Կարող եք փորձարկել հարցման արտահայտությունները և տեսնել արդյունքների տարբերությունները: Այս ուղեցույցը ցույց է տալիս C# լեզվի առանձնահատկությունները, որոնք օգտագործվում են LINQ հարցման արտահայտություններ գրելու համար:

### Հիշողության մեջ տվյալների աղբյուրի ստեղծում

Հարցումների տվյալների աղբյուրը Ուսանողի գրառումների պարզ ցանկ է: Ուսանողի յուրաքանչյուր գրառում ունի անուն, ազգանուն և ամբողջ թվերի զանգված, որը ներկայացնում է նրանց թեստերի միավորները:

```c#
IEnumerable<Student> students =
[
    new Student(First: "Svetlana", Last: "Omelchenko", ID: 111, Scores: [97, 92, 81, 60]),
    new Student(First: "Claire",   Last: "O'Donnell",  ID: 112, Scores: [75, 84, 91, 39]),
    new Student(First: "Sven",     Last: "Mortensen",  ID: 113, Scores: [88, 94, 65, 91]),
    new Student(First: "Cesar",    Last: "Garcia",     ID: 114, Scores: [97, 89, 85, 82]),
    new Student(First: "Debra",    Last: "Garcia",     ID: 115, Scores: [35, 72, 91, 70]),
    new Student(First: "Fadi",     Last: "Fakhouri",   ID: 116, Scores: [99, 86, 90, 94]),
    new Student(First: "Hanying",  Last: "Feng",       ID: 117, Scores: [93, 92, 80, 87]),
    new Student(First: "Hugo",     Last: "Garcia",     ID: 118, Scores: [92, 90, 83, 78]),

    new Student("Lance",   "Tucker",      119, [68, 79, 88, 92]),
    new Student("Terry",   "Adams",       120, [99, 82, 81, 79]),
    new Student("Eugene",  "Zabokritski", 121, [96, 85, 91, 60]),
    new Student("Michael", "Tucker",      122, [94, 92, 91, 91])
];
```

- Ուսանողների հաջորդականությունը ինիցիալիզացվում է Collection expression-ի միջոցով։
- Students փոփոխականը պարունակում է այս օրինակում օգտագործված բոլոր Student օրինակների ցանկը։
- Կոնստրուկտորի որոշ կանչեր օգտագործում են անվանված արգումենտներ՝ պարզաբանելու համար, թե որ արգումենտն է համապատասխանում կոնստրուկտորի որ պարամետրին։

### Հարցման ստեղծում

Հարցման կատարման արդյունքում կունենանք բոլոր այն ուսանողների ցանկը, որոնց միավորները առաջին թեստում 90-ից մեծ էին։ Քանի որ ընտրված է ամբողջ Student օբյեկտը, հարցման տեսակը IEnumerable<Student> է։

<div style="padding: 10px; border: 1px solid #2196F3; background-color: #E3F2FD;">
  <strong>ℹ️ Info:</strong> IEnumerable -ը C# ինտերֆեյս է, որը ներկայացնում է տարրերի հաջորդականություն, որոնք կարող են թվարկվել (իտերացվել) մեկ առ մեկ։ Այլ կերպ ասած ցանկացած դաս, որը իրականացնում է այս ինտերֆեսյսը կարող օգտագործվել foreach ցիկլում։
</div>
<br/>

Չնայած կոդը կարող է նաև օգտագործել անուղղակի տիպավորում՝ օգտագործելով **var** բանալի բառը, ակնհայտ տիպավորումն օգտագործվում է արդյունքները հստակ պատկերելու համար։

```c#
// Հարցման ստեղծում
// Առաջին տողը կարող էր նաև գրված լինել այսպես՝ "var studentQuery ="
IEnumerable<Student> studentQuery =
    from student in students
    where student.Scores[0] > 90 // կընտրվեն այն ուսանողները որոնց առաջին թեստի գնահատականը մեծ է 90 -ից
    select student;
```

Հարցման միջակայքի փոփոխականը՝ student-ը, ծառայում է որպես հղում աղբյուրի յուրաքանչյուր Student-ի համար։

### Հարցման կատարում

Հիմա գրենք foreach ցիկլը, որը կհանգեցնի հարցման կատարմանը: Վերադարձված հաջորդականության յուրաքանչյուր տարրին հասանելիությունը կատարվում է foreach ցիկլի իտերացիոն փոփոխականի միջոցով: Այս փոփոխականի տիպը Student է, իսկ հարցման փոփոխականի տեսակը՝ համատեղելի՝ IEnumerable<Student>:

```c#
// Հարցման կատարում
// Student-ի փոխարեն կարող էր օգտագործվել  նաև var
foreach (Student student in studentQuery)
{
    Console.WriteLine($"{student.Last}, {student.First}");
}

// Դուրս բերվող տեքստ:
// Omelchenko, Svetlana
// Garcia, Cesar
// Fakhouri, Fadi
// Feng, Hanying
// Garcia, Hugo
// Adams, Terry
// Zabokritski, Eugene
// Tucker, Michael

```

Հարցման where պայմանում հնարավոր է համատեղել մի քանի բուլյան պայմաններ։ Հետևյալ կոդը ավելացնում է պայման, որպեսզի հարցումը վերադարձնի այն ուսանողներին, որոնց առաջին միավորը 90-ից բարձր էր, իսկ վերջինը՝ 80-ից ցածր։ 

```c#
where student.Scores[0] > 90 && student.Scores[3] < 80  
```

### Հարցման արդյունքների դասավորում

Հարցման արդյունքների հետ ավելի հարմար է աշխատել, եթե դրանք դասավորված են որոշակի հերթականությամբ։ Դուք կարող եք վերադարձված հաջորդականությունը դասավորել աղբյուրի տարրերի ցանկացած հասանելի դաշտով։ Օրինակ, հետևյալ orderby կետը արդյունքները դասավորում է այբբենական կարգով՝ A-ից Z՝ ըստ յուրաքանչյուր ուսանողի ազգանվան։ Ավելացրեք հետևյալ orderby կետը ձեր հարցման where հրամանից անմիջապես հետո և select հրամանից առաջ։

```c#
    orderby student.Last ascending
```

orderby պայմանի միջոցով հնարավոր է արդյունքները դասավորել հակառակ հերթականությամբ՝ առաջին թեստի միավորների համաձայն՝ ամենաբարձր միավորից մինչև ամենացածրը։

```c#
orderby student.Scores[0] descending
```

### Արդյունքների խմբավորում

Խմբավորման արդյունքում ստեղծում է խմբերի հաջորդականություն, և յուրաքանչյուր խումբ ինքնին պարունակում է Բանալի և հաջորդականություն, որը բաղկացած է այդ խմբի բոլոր անդամներից: Հետևյալ նոր հարցումը խմբավորում է ուսանողներին՝ որպես բանալի օգտագործելով նրանց ազգանվան առաջին տառը։ 

```c#
IEnumerable<IGrouping<char, Student>> studentQuery =
    from student in students
    group student by student.Last[0];
```

Հարցման տեսակը փոխվեց։ Այն այժմ ստեղծում է խմբերի հաջորդականություն, որոնք որպես բանալի ունեն char տեսակը, և Student օբյեկտների հաջորդականություն։ Foreach կատարման ցիկլի կոդը նույնպես պետք է փոխվի։

```c#
foreach (IGrouping<char, Student> studentGroup in studentQuery)
{
    Console.WriteLine(studentGroup.Key);
    foreach (Student student in studentGroup)
    {
        Console.WriteLine($"   {student.Last}, {student.First}");
    }
}
// Ելքագրում:
// O
//   Omelchenko, Svetlana
//   O'Donnell, Claire
// M
//   Mortensen, Sven
// G
//   Garcia, Cesar
//   Garcia, Debra
//   Garcia, Hugo
// F
//   Fakhouri, Fadi
//   Feng, Hanying
// T
//   Tucker, Lance
//   Tucker, Michael
// A
//   Adams, Terry
// Z
//   Zabokritski, Eugene

```

IGroupings-ի IEnumerables-ի բացահայտ նշելու փախարեն Նույն հարցումը և foreach ցիկլը շատ ավելի հարմար է գրել՝ օգտագործելով var -ը: Var բանալի բառը չի փոխում ձեր օբյեկտների տեսակները. այն պարզապես հրահանգում է կոմպիլյատորին եզրակացնել տեսակները:

```c#
public record Student(string First, string Last, int ID, int[] Scores);
class Program()
{
    static void Main()
    {
        IEnumerable<Student> students = [
            new Student(First: "Svetlana", Last: "Omelchenko", ID: 111, Scores: [97, 92, 81, 60]),
            new Student(First: "Claire",   Last: "O'Donnell",  ID: 112, Scores: [75, 84, 91, 39]),
            new Student(First: "Sven",     Last: "Mortensen",  ID: 113, Scores: [88, 94, 65, 91]),
            new Student(First: "Cesar",    Last: "Garcia",     ID: 114, Scores: [97, 89, 85, 82]),
            new Student(First: "Debra",    Last: "Garcia",     ID: 115, Scores: [35, 72, 91, 70]),
            new Student(First: "Fadi",     Last: "Fakhouri",   ID: 116, Scores: [99, 86, 90, 94]),
            new Student(First: "Hanying",  Last: "Feng",       ID: 117, Scores: [93, 92, 80, 87]),
            new Student(First: "Hugo",     Last: "Garcia",     ID: 118, Scores: [92, 90, 83, 78]),

            new Student("Lance",   "Tucker",      119, [68, 79, 88, 92]),
            new Student("Terry",   "Adams",       120, [99, 82, 81, 79]),
            new Student("Eugene",  "Zabokritski", 121, [96, 85, 91, 60]),
            new Student("Michael", "Tucker",      122, [94, 92, 91, 91])
        ];
        var studentQuery =
                from student in students
                where student.Scores[0] > 90 
                select students;

        var studentGroup =
            from student in students
            group student by student.Last[0];

        foreach (var group in studentGroup)
        {
            Console.WriteLine($"Group: {group.Key}");
            foreach (var student in group)
            {
                Console.WriteLine($"{student.Last}, {student.First}");
            }
        }
        Console.WriteLine(studentQuery.ToString());
    }

}
// Ելքագրում:
// O
//   Omelchenko, Svetlana
//   O'Donnell, Claire
// M
//   Mortensen, Sven
// G
//   Garcia, Cesar
//   Garcia, Debra
//   Garcia, Hugo
// F
//   Fakhouri, Fadi
//   Feng, Hanying
// T
//   Tucker, Lance
//   Tucker, Michael
// A
//   Adams, Terry
// Z
//   Zabokritski, Eugene
```

### Դասավորում ըստ բանալու և արժեքի

Նախորդ հարցման մեջ խմբերը այբբենական կարգով չեն դասավորված։ Դուք կարող եք group պայմանից հետո տեղադրել orderby կետ։ Սակայն orderby կետն օգտագործելու համար ձեզ նախ անհրաժեշտ է նույնականացուցիչ, որը կծառայի որպես հղում group կետի կողմից ստեղծված խմբերին։ Դուք նույնականացուցիչը տրամադրում եք into բանալի բառի միջոցով՝ հետևյալ կերպ.

```c#
var studentQuery4 =
    from student in students
    group student by student.Last[0] into studentGroup
    orderby studentGroup.Key
    select studentGroup;

foreach (var groupOfStudents in studentQuery4)
{
    Console.WriteLine(groupOfStudents.Key);
    foreach (var student in groupOfStudents)
    {
        Console.WriteLine($"   {student.Last}, {student.First}");
    }
}

// Ելքագրում:
//A
//   Adams, Terry
//F
//   Fakhouri, Fadi
//   Feng, Hanying
//G
//   Garcia, Cesar
//   Garcia, Debra
//   Garcia, Hugo
//M
//   Mortensen, Sven
//O
//   Omelchenko, Svetlana
//   O'Donnell, Claire
//T
//   Tucker, Lance
//   Tucker, Michael
//Z
//   Zabokritski, Eugene

```

Այժմ հարցման արդյունքում խմբերը դասավորված կլինեն այբբենական կարգով։

Հնարավոր է հարցման արտահայտության մեջ օգտագործել let բանալի բառը, որպես ցանկացած արտահայտության արդյունքի նույնականացուցիչ։ Այս նույնականացուցիչը կարող է հարմար լինել, ինչպես ներկայացված է հետևյալ օրինակում։ Այն կարող է նաև բարելավել արդյունավետությունը՝ պահպանելով արտահայտության արդյունքները, որպեսզի այն բազմիցս հաշվարկելու կարիք չլինի։

```c#
// Այս հարցումը վերադարձնում է այն ուսանողներին որոնց
// առաջին թեստի արդյունքը ավելի բարձր է քան նրանց միջին գնահատականը
var studentQuery5 =
    from student in students
    let totalScore = student.Scores[0] + student.Scores[1] +
        student.Scores[2] + student.Scores[3]
    where totalScore / 4 < student.Scores[0]
    select $"{student.Last}, {student.First}";

foreach (string s in studentQuery5)
{
    Console.WriteLine(s);
}

// Ելքագրում:
// Omelchenko, Svetlana
// O'Donnell, Claire
// Mortensen, Sven
// Garcia, Cesar
// Fakhouri, Fadi
// Feng, Hanying
// Garcia, Hugo
// Adams, Terry
// Zabokritski, Eugene
// Tucker, Michael
```

### Մեթոդի շարահյուսության օգտագործում հարցման արտահայտության մեջ

Որոշ հարցման գործողություններ կարող են արտահայտվել միայն մեթոդի սինտաքսի միջոցով: Հետևյալ կոդը հաշվարկում է սկզբնական հաջորդականության յուրաքանչյուր ուսանողի համար ընդհանուր միավորը, ապա կանչում է այդ հարցման արդյունքների վրա հիմնված Average() մեթոդը՝ դասարանի միջին միավորը հաշվարկելու համար:

```c#
var studentQuery =
    from student in students
    let totalScore = student.Scores[0] + student.Scores[1] +
        student.Scores[2] + student.Scores[3]
    select totalScore;

double averageScore = studentQuery.Average();
Console.WriteLine($"Class average score = {averageScore}");

// Ելքագրում:
// Class average score = 334.166666666667
```

### Փոխակերպում կամ արտապատկերում select արտահայտության մեջ

Հաճախ հարցման մեջ առաջանում է հաջորդականություն, որի տարրերը տարբերվում են սկզբնական հաջորդականությունների տարրերից: Հետևյալ հարցումը վերադարձնում է տողերի հաջորդականություն (ոչ թե Students-ների):

```c#
IEnumerable<string> studentQuery =
    from student in students
    where student.Last == "Garcia"
    select student.First;

Console.WriteLine("The Garcias in the class are:");
foreach (string s in studentQuery)
{
    Console.WriteLine(s);
}

// Ելքագրում:
// The Garcias in the class are:
// Cesar
// Debra
// Hugo
```

Ուսանողների հաջորդականություն ստանալու համար, որոնց ընդհանուր միավորը մեծ է դասարանի միջինից, նրանց ուսանողի ID-ի հետ միասին, կարող եք օգտագործել անանուն տիպ select հրամանում.

```c#
var aboveAverageQuery =
    from student in students
    let x = student.Scores[0] + student.Scores[1] +
        student.Scores[2] + student.Scores[3]
    where x > averageScore
    select new { id = student.ID, score = x };

foreach (var item in aboveAverageQuery)
{
    Console.WriteLine("Student ID: {0}, Score: {1}", item.id, item.score);
}

// Ելքագրում:
// Student ID: 113, Score: 338
// Student ID: 114, Score: 353
// Student ID: 116, Score: 369
// Student ID: 117, Score: 352
// Student ID: 118, Score: 343
// Student ID: 120, Score: 341
// Student ID: 122, Score: 368

```
