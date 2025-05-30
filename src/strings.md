# Աշխատանք տողերի հետ

## Բովանդակություն

- [Աշխատանք տողերի հետ](#աշխատանք-տողերի-հետ)
  - [Բովանդակություն](#բովանդակություն)
  - [Տողեր և տողային լիտերալներ](#տողեր-և-տողային-լիտերալներ)
  - [Տողերի հայտարարում և ինիցիալիզացիա](#տողերի-հայտարարում-և-ինիցիալիզացիա)
  - [Տողերի անփոփոխություն](#տողերի-անփոփոխություն)
  - [Quoted string literals](#quoted-string-literals)
  - [Verbatim string literals](#verbatim-string-literals)
  - [Raw string literals](#raw-string-literals)
  - [Format strings](#format-strings)
    - [Տողերի ինտերպոլյացիա (String interpolation)](#տողերի-ինտերպոլյացիա-string-interpolation)
      - [Verbatim string interpolation](#verbatim-string-interpolation)
    - [Կոմպոզիցիոն ձևաչափում (Composite formatting)](#կոմպոզիցիոն-ձևաչափում-composite-formatting)
  - [Ենթատողեր (Substrings)](#ենթատողեր-substrings)
  - [Հասանելիություն տողի առանձին սիմվոլների](#հասանելիություն-տողի-առանձին-սիմվոլների)
  - [Null արժեքով տողեր և դատարկ տողեր (Null strings and empty strings)](#null-արժեքով-տողեր-և-դատարկ-տողեր-null-strings-and-empty-strings)
  - [StringBuilder-ի օգտագործում տողերի արագ ստեղծման համար](#stringbuilder-ի-օգտագործում-տողերի-արագ-ստեղծման-համար)

## Տողեր և տողային լիտերալներ

Տողը String տիպի օբյեկտ է, որի արժեքը տեքստ է: Ներքին, տեքստը պահվում է որպես Char օբյեկտների հաջորդական, միայն կարդալու համար նախատեսված հավաքածու: Տողերի Length հատկությունը ներկայացնում է Char օբյեկտների քանակը, որը Unicode նիշերի թիվն է:

[Strings and string literals](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/strings/)

## Տողերի հայտարարում և ինիցիալիզացիա

Տողեր հնարավոր է հայտարարել և ինիցիալիզացնել տարբեր ձևերով։

```c#
//1.  հայտարարում առանց ինիցիալիզացիայի
string message1;

//2. Ինիցիալիզացում null արժեքով
string? message2 = null;

//3. Ինիցիալիզացում դատարկ տողի արժեքով

string message3 = "";

//4. Ինիցիալիզացում տողային լիտերալով. **
string oldPath = "c:\\Program Files\\Microsoft Visual Studio 8.0";

//5. Ինիցիալիզացում verbatim տողային լիտերալով.
string newPath = @"c:\Program Files\Microsoft Visual Studio 9.0";

//6. Անուղակի վերագրում (փոփոխականի տիպը կորոշի կոմպիլյատորը)
var temp = "I'm still a strongly-typed System.String!";

```

**Ինչու՞ է 4-րդ օրինակում օգտագործվում կրկնակի հակառակ շեղատող \\\ **

C# լեզվում հակառակ շեղատողը (\\) հատուկ նշան է, որը նշում է, որ հետևող սիմվոլը հատուկ նշանակություն ունի։ Օրինակ՝

```
    \n — նոր տող,
    \t — tab (հատվածային բացատ),
    \\ — բառացի հակառակ շեղատող (այսինքն՝ պարզապես \ սիմվոլ)։
```

Քանի որ Windows-ում ֆայլերի ճանապարհմերը սովորաբար նշվում են հակառակ շեղատողով, օրինակ՝ C:\Program Files\..., իսկ C#-ում մեկ շեղատողը սպասում է escape հաջորդականություն, անհրաժեշտ է յուրաքանչյուր հակառակ շեղատողը կրկնել, այսինքն՝ գրել \\։

Եթե տեքստը պարունակում է հակառակ շեղատողի (\\) սիմվոլներ հնարավոր է նաև օգտագործել **verbatim string literal** (բառացի տեքստ) escape նշաններից խուսափելու համար, այնպես ինչպես ցուցադրված է Օրինակ 5-ում։

## Տողերի անփոփոխություն

Տողերը անփոփոխ են։ Դրանք չեն կարող փոխվել ստեղծվելուց հետո: Բոլոր **String** մեթոդները և C# օպերատորները, որոնք կարծես փոփոխում են տողը, իրականում վերադարձնում են նոր օբյեկտ:

Քանի որ տողի «փոփոխությունը» իրականում նոր տողի ստեղծում է, տողերին հղումներ ստեղծելիս պետք է զգույշ լինել։ Եթե տողի հղում եք ստեղծում, այնուհետև «փոփոխում» եք սկզբնական տողը, հղումը շարունակում է մատնանշել սկզբնական օբյեկտին, այլ ոչ թե այն նոր օբյեկտին, որը ստեղծվել էր տողի փոփոխության ժամանակ։

```c#

string str1 = "Hello ";
string str2 = str1; // str2 -ին վերագրվում է str1 փոփոխականում պահվող տող տեսակի օբյեկտի հղումը 


/* Ստեղծվում է նոր, "Hello World" տողը պարունակող, տող տեսակի օբյեկտ, որի հղումը վերագրվում է str1 փոփոխականին։ Այսպիսով str1-ի հղումը փոխվեց այն դեպքում երբ str2 -ը պարունակում սկզբնական օբյեկտի հղումը */ 
str1 += "World"; 

System.Console.WriteLine(str2); // դուրս բերվող արժեք՝ Hello

```

## Quoted string literals

Այս տեսակի տողային լիտերալները սկսվում և ավարտվում են չակերտի (") նշանով։ Այս տեսակի լիտերալների օգտագործումը հարմար է այն դեպքում երբ տողային լիտերալը մեկ տողանի է և չի պարունակում escape հաջորդականություններ։

```c#

string s1 = "Hello world"; // escape հաջորդականություն չպարունակող տող

string columns = "Column 1\tColumn 2\tColumn 3";
//դուրս բերվող արժեք՝ Column 1        Column 2        Column 3

string rows = "Row 1\r\nRow 2\r\nRow 3";
/* դուրս բերվող արժեք՝
    Row 1
    Row 2
    Row 3
*/

string title = "\"The \u00C6olean Harp\", by Samuel Taylor Coleridge";
//դուրս բերվող արժեք՝ "The Æolean Harp", by Samuel Taylor Coleridge

```

[scape sequences](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/strings/#string-escape-sequences)

## Verbatim string literals

Այս տեսակի օգտագործումը հարմար է երբ լիտերալը բազմատող է կամ ներառում է չակերտի նշաններ ("")։
Օգտագործեք կրկնակի չակերտներ՝ լիտերալի տողի մեջ չակերտը տեղադրելու համար:

```c#
string filePath = @"C:\Users\scoleridge\Documents\";
//դուրս բերվող արժեք՝ C:\Users\scoleridge\Documents\

string text = @"My pensive SARA ! thy soft cheek reclined
    Thus on mine arm, most soothing sweet it is
    To sit beside our Cot,...";
/* դուրս բերվող արժեք՝
My pensive SARA ! thy soft cheek reclined
    Thus on mine arm, most soothing sweet it is
    To sit beside our Cot,...
*/

string quote = @"Her name was ""Sara.""";
//դուրս բերվող արժեք՝ Her name was "Sara."
```

## Raw string literals

Այս տեսակի լիտերալների օգտագործումը հարմար է բազմատող տողերի դեպքում, բացի այդ այն վերացնում է escape sequence-ների օգտագործման անհրաժեշտությունը։ Բացատները (spaces, tabs, newlines...) որոնք օգտագործվել են լիտերակում կարտացոլվեն ելքագրվող տողում։

**Raw string literal - ների ստեղծման կանոնները**

- Սկսվում և ավարտվում է առնվազն երեք կրկնակի չակերտների հաջորդականությամբ ("""): Դուք կարող եք օգտագործել երեքից ավելի հաջորդական նիշեր՝ հաջորդականությունը սկսելու և ավարտելու համար՝ ապահովելու համար տողային լիտերալներ, որոնք պարունակում են երեք (կամ ավելի) կրկնվող չակերտների նիշեր:
- Միատող լիտերալները պահանջում են բացման և փակման չակերտների նիշեր նույն տողում:
- Բազմատող լիտերալները պահանջում են ինչպես բացման, այնպես էլ փակման չակերտների նիշեր իրենց առանձին տողում:
- Բազմատող լիտերալներում փակման չակերտներից ձախ գտնվող ցանկացած սպիտակ տարածություն (white space) հեռացվում է բոլոր տողերից:
- Բազմատող լիտերալներում բացման չակերտին հաջորդող սպիտակ տարածությունը անտեսվում է:
- Բազմատող լիտերալներում բացման չակերտին հաջորդող դատարկ տողերը ներառված են տողային լիտերալում:

```c#
string singleLine = """Friends say "hello" as they pass by.""";
string multiLine = """
    "Hello World!" is typically the first program someone writes.
    """;
string embeddedXML = """
       <element attr = "content">
           <body style="normal">
               Here is the main text
           </body>
           <footer>
               Excerpts from "An amazing story"
           </footer>
       </element >
       """;
// "<element attr = "content"> տողը սկսվում է առաջին սյունակից։
// Բոլոր բացատները որոնք գտնվում են այդ սյունակից ձախ կհեռացվեն։

string rawStringLiteralDelimiter = """"
    Raw string literals are delimited 
    by a string of at least three double quotes,
    like this: """
    """";
```

Ստորև բերված օրինակում ներկայացվում են սխալներ, որոնք կարող են առաջանալ վերևում նշված կանոնները չպահպանելու դեպքում։

```c#
// CS8997: Unterminated raw string literal.
var multiLineStart = """This
    is the beginning of a string 
    """;

// CS9000: Raw string literal delimiter must be on its own line.
var multiLineEnd = """
    This is the beginning of a string """;

/* Վերևի երկու օրինակներում սխալի պատճառն է բազմատող լիտերալի բացվող և փակվող 
    չակերտների հաջորդականությունը (""") առանձին տողում գրված չլինելը։ */


// CS8999: Line does not start with the same whitespace as the closing line
// of the raw string literal
var noOutdenting = """
    A line of text.
Trying to outdent the second line.
    """;

/* Երկրորդ տողի սկիզբը պետք է լինի ուղահայաց նույն մակարդակի վրա։

Այսպես՝
var noOutdenting = """
    A line of text.
    Trying to outdent the second line.
    """;
*/

```

## Format strings

Format string -ը տող է, որի պարունակությունը որոշվում է կատարման ժամանակ, դինամիկ կերպով։ Ձևաչափի տողերը ստեղծվում են տողի մեջ ձևավոր փակագծերում ինտերպոլացված արտահայտություններ կամ տեղապահներ (placeholders) տեղադրելով։ Փակագծերի ({...}) ներսում գտնվող ամեն ինչ վերածվում է արժեքի, որը այնուհետև մասնակցում է տողի ձևավորման համար։  

Կա Ձևաչափի տողեր ստեղծելու երկու մեթոդ՝

- տողերի ինտերպոլյացիա (String interpolation)
- կոմպոզիտային ձևաչափում (Composite formatting)

### Տողերի ինտերպոլյացիա (String interpolation)

Ինտերպոլացված տողերը հայտարարվում են $ հատուկ նիշով: Նրանք ներառում է ինտերպոլացված արտահայտություններ, որոնք գրվում են ձևավոր փակագծերում ({}):

Ինտերպոլացված արտահայտությունները վերածվում են արժեքի, որը կիրառվում է տողի ձևավորման համար:

```c#
var jh = (firstName: "Jupiter", lastName: "Hammon", born: 1711, published: 1761);

// Jupiter Hammon was an African American poet born in 1711.
Console.WriteLine($"{jh.firstName} {jh.lastName} was an African American poet born in {jh.born}.");

// He was first published in 1761 at the age of 50.
Console.WriteLine($"He was first published in {jh.published} at the age of {jh.published - jh.born}.");

// He'd be over 300 years old today.
Console.WriteLine($"He'd be over {Math.Round((2018d - jh.born) / 100d) * 100d} years old today.");
```

#### Verbatim string interpolation

Ինտերպոլացված verbatim տողը սկսվում է $ նիշով, որին հաջորդում է @ նիշը։ Դուք կարող եք օգտագործել $ և @ տոկենները ցանկացած հերթականությամբ. և՛ $@"...", և՛ @$"... վավեր ինտերպոլացված verbatim տողեր են։

```c#
var jh = (firstName: "Jupiter", lastName: "Hammon", born: 1711, published: 1761);

//Jupiter Hammon
//     was an African American poet born in 1711.

Console.WriteLine($@"{jh.firstName} {jh.lastName}
    was an African American poet born in {jh.born}.");

// He was first published in 1761
// at the age of 50.
Console.WriteLine(@$"He was first published in {jh.published}
at the age of {jh.published - jh.born}.");

```

### Կոմպոզիցիոն ձևաչափում (Composite formatting)

The String.Format-ն օգտագործում է փակագծերում տեղապահներ (placeholders)՝ ձևաչափի տող ստեղծելու համար: Այս օրինակի արդյունքը նույն է նախորդ նմուշում օգտագործված տողային ինտերպոլացիայի մեթոդին:

```c#
var pw = (firstName: "Phillis", lastName: "Wheatley", born: 1753, published: 1773);
Console.WriteLine("{0} {1} was an African American poet born in {2}.", pw.firstName, pw.lastName, pw.born);
Console.WriteLine("She was first published in {0} at the age of {1}.", pw.published, pw.published - pw.born);
Console.WriteLine("She'd be over {0} years old today.", Math.Round((2018d - pw.born) / 100d) * 100d);
```

## Ենթատողեր (Substrings)

Ենթատողը տողում պարունակվող նիշերի ցանկացած հաջորդականություն է: Օգտագործեք Substring մեթոդը՝ սկզբնական տողի մի մասից նոր տող ստեղծելու համար: Հնարավոր է որոնել ենթատողի մեկ կամ մի քանի դեպքեր՝ օգտագործելով **IndexOf** մեթոդը: Օգտագործեք **Replace** մեթոդը՝ նշված ենթատողի բոլոր դեպքերը նոր տողով փոխարինելու համար: Ինչպես **Substring** մեթոդը, **Replace**-ը իրականում վերադարձնում է նոր տող և չի փոփոխում սկզբնական տողը: 

```c#
string s3 = "Visual C# Express";
System.Console.WriteLine(s3.Substring(7, 2)); // Վերցնում է սահմանված տողի 7-րդ սիմվոլից սկսած երկու հաջորդական նիշերը
// Ելքագրվող արժեք՝ "C#"

System.Console.WriteLine(s3.Replace("C#", "Basic")); // Փոխարինում է "C#" ենթատողը "Basic" ենթատողով
// Ելքագրվող արժեք՝ "Visual Basic Express"

int index = s3.IndexOf("C"); // Վերադարձնում է "C" սիմվոլի ինդեքսը (հերթական համարը) տողում։ Ինդեքսի հաշվարկը սկսվում է 0-ից
// index = 7

```

## Հասանելիություն տողի առանձին սիմվոլների

Դուք կարող եք օգտագործել քառակուսի փակագծեը ([]) ինդեքսի արժեքով` առանձին նիշերի միայն ընթերցման հասանելիություն ստանալու համար։

```c#
string s5 = "Printing backwards";

for (int i = 0; i < s5.Length; i++)
{
    /* s5[s5.Length - i - 1] -ն հաշվարկվում է հերթական սիմվոլի ինդեքսը տողի վերրջից, տողի երկարությունից հանելով հերթական ինդեքսի թիվը, այնուհետև հանելով ևս 1։ Վեջինը հանվում է քանի որ ինդեքսների հաշվարկը սկսվում է 0-ից։
    */
    System.Console.Write(s5[s5.Length - i - 1]); 
}
// դուրս բերվող արժեք՝ "sdrawkcab gnitnirP"

```

## Null արժեքով տողեր և դատարկ տողեր (Null strings and empty strings)

Դատարկ տողը System.String օբյեկտի օրինակ է, որը պարունակում է զրո նիշ։ Դատարկ տողերը հաճախ օգտագործվում են տարբեր ծրագրավորման սցենարներում՝ դատարկ տեքստային դաշտ ներկայացնելու համար։ Դուք կարող եք կանչել մեթոդներ դատարկ տողերի վրա, քանի որ դրանք վավեր System.String օբյեկտներ են։ Դատարկ տողերը նախնականացվում են հետևյալ կերպ՝

```c#
string s = String.Empty;
```

Ի տարբերություն դրա, null տողը չի վերաբերում System.String օբյեկտի օրինակին, և null տողի վրա մեթոդ կանչելու ցանկացած փորձ առաջացնում է NullReferenceException: Այնուամենայնիվ, դուք կարող եք օգտագործել null տողերը այլ տողերի հետ միացման և համեմատության գործողություններում: Հետևյալ օրինակները ցույց են տալիս որոշ դեպքեր, երբ null տողի հղումը առաջացնում է և չի առաջացնում բացառություն (exception)։

```c#
string str = "hello";
string? nullStr = null;
string emptyStr = String.Empty;

string tempStr = str + nullStr;
// դուրս բերվող արժեք՝  hello
Console.WriteLine(tempStr);

bool b = (emptyStr == nullStr);
// դուրս բերվող արժեք՝  False
Console.WriteLine(b);

// Ստորև օրինակը կստեղծի նոր դատարկ տող
string newStr = emptyStr + nullStr;

// Null և դատարկ տողերը ունեն տարբեր պահվածք.
// հաջորդող երկու տողերը կցուցադրեն 0 արժեքը

Console.WriteLine(emptyStr.Length);
Console.WriteLine(newStr.Length);

// այս տողը կառաջացնի NullReferenceException.
Console.WriteLine(nullStr.Length);

// դուրս բերվող արժեք՝  4
Console.WriteLine(s2.Length);

```

## StringBuilder-ի օգտագործում տողերի արագ ստեղծման համար

NET-ում տողային գործողությունները բարձր օպտիմիզացված են և շատ դեպքերում էականորեն չեն ազդում արդյունավետության վրա: Այնուամենայնիվ, որոշ սցենարներում, ինչպիսիք են հարյուրավոր կամ հազարավոր անգամներ կատարվող ցիկլերում, տողային գործողությունները կարող են ազդել արդյունավետության վրա: **StringBuilder** դասը ստեղծում է տողային բուֆեր, որն ապահովում է ավելի լավ արդյունավետություն, եթե ձեր ծրագիրը կատարում է տողերի բազմաթիվ մանիպուլյացիաներ: **StringBuilder** տողը նաև թույլ է տալիս վերաբաշխել առանձին նիշեր, ինչը հնարավոր չէ տողային  տեսակի դեպքում:

Ստորև բերված օրինակում կատարվում է տողի փոփոխություն առանց նոր տող ստեղծելու:

```c#
System.Text.StringBuilder sb = new System.Text.StringBuilder("Rat: the ideal pet");
sb[0] = 'C';
System.Console.WriteLine(sb.ToString());
//Outputs Cat: the ideal pet

```

Այս օրինակում StringBuilder օբյեկտը օգտագործվում է մի շարք թվային տեսակներից տող ստեղծելու համար.

```c#
var sb = new StringBuilder();

// Ստեղծում է տող որը բաղկացած է 0-9 թվերից
for (int i = 0; i < 10; i++)
{
    sb.Append(i.ToString());
}
Console.WriteLine(sb);  // 0123456789

// Տողի սիմվոլի պատճենում (հնարավոր չէ System.String դեպքում)
sb[0] = sb[9];

Console.WriteLine(sb);  // 9123456789

```
