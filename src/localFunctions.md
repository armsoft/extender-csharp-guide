# Լոկալ ֆունկցիաներ

## Բովանդակություն

- [Լոկալ ֆունկցիաներ](#լոկալ-ֆունկցիաներ)
  - [Բովանդակություն](#բովանդակություն)
  - [Լոկալ ֆունկցիաների շարահյուսություն](#լոկալ-ֆունկցիաների-շարահյուսություն)
  - [Expression-bodied members](#expression-bodied-members)
  - [Լոկալ ֆունկցիաներ և լամբդա արտահայտություններ](#լոկալ-ֆունկցիաներ-և-լամբդա-արտահայտություններ)
    - [Անվանակոչում](#անվանակոչում)
    - [Բացահայտ վերագրում](#բացահայտ-վերագրում)
    - [Variable capture](#variable-capture)

Լոկալ ֆունկցիաները մեկ այլ անդամի (մեթոդներ, կոնստրուկտորներ, հատկություններ, լամբդա արտահայտություններ, այլ լոկալ ֆունկցիաներ) մեջ ներդրված տեսակի մեթոդներ են։ Դրանք կարող են կանչվել միայն իրենց պարունակող անդամից։  

## Լոկալ ֆունկցիաների շարահյուսություն

[Local function syntax](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/local-functions#local-function-syntax)

Լոկալ ֆունկցիան սահմանվում է որպես պարունակող անդամի ներսում ներդրված մեթոդ։ Դրանց սահմանումն ունի հետևյալ շարահյուսությունը՝

`<մոդիֆիկատոր> <վերադարձվող-տիպ> <ֆունկցիայի-անուն> <պարամետրերի-ցուցակ>`

Հնարավոր է օգտագործել այնպիսի մոդիֆիկատորներ ինչպիսին են՝ `async` կամ `static`

Բոլոր լոկալ փոփոխականները, որոնք սահմանված են պարունակող անդամում, ներառյալ դրա մեթոդի պարամետրերը, հասանելի են ոչ ստատիկ լոկալ ֆունկցիայում։

Հետևյալ օրինակը սահմանում է `AppendPathSeparator` անունով լոկալ ֆունկցիա, որը հասանելի է միայն GetText անունով մեթոդի համար։

```c#
private static string GetText(string path, string filename)
{
     var reader = File.OpenText($"{AppendPathSeparator(path)}{filename}");
     var text = reader.ReadToEnd();
     return text;

     string AppendPathSeparator(string filepath)
     {
        // Ավելացվում է \ նշանը եթե այն առկա չէ ճանապարհի վերջում
        return filepath.EndsWith(@"\") ? filepath : filepath + @"\";
     }
}
```

## Expression-bodied members

[Expression-bodied members](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/expression-bodied-members)

Բերված օրինակներում կիրատռվել է `expression-bodied` սահմանում։ Դուք կարող եք օգտագործել այս տեսակի սահմանումը, երբ  ֆունկցիայի, մեթոդի կամ հատկության տրամաբանությունը բաղկացած է մեկ արտահայտությունից: Հակառակ դեպքում անհրաժեշտ է օգտագործել ձևավոր փակագծեր `{}`։

```c#
    int nthFactorial(int number) => number < 2 
        ? 1 
        : number * nthFactorial(number - 1);
```

և

```c#
    int nthFactorial(int number) 
    {
       number < 2 
        ? 1 
        : number * nthFactorial(number - 1);
    }
```

գրելաձևերը հավասարազոր են։

## Լոկալ ֆունկցիաներ և լամբդա արտահայտություններ

[Local functions vs. lambda expressions](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/local-functions#local-functions-vs-lambda-expressions)

Առաջին հայացքից, լոկալ ֆունկցիաները և լամբդա արտահայտությունները նման են։ Շատ դեպքերում, լամբդա արտահայտությունների և լոկալ ֆունկցիաների միջև ընտրությունը ոճի և անձնական նախասիրության հարց է։ Այնուամենայնիվ, կան իրական տարբերություններ այն հարցում, թե որտեղ կարող եք օգտագործել մեկը կամ մյուսը, որոնց մասին պետք է տեղյակ լինեք։

Դիտարկենք ֆակտորիալի ալգորիթմի լոկալ ֆունկցիայի և լամբդա արտահայտության իրականացումների միջև եղած տարբերությունները։

```c#
// Լոկալ ֆունկցիայի տարբերակ
public static int LocalFunctionFactorial(int n)
{
    return nthFactorial(n);

    int nthFactorial(int number) => number < 2 
        ? 1 
        : number * nthFactorial(number - 1);
}
```

```c#
// Լամբդա արտահայության տարբերակ
public static int LambdaFactorial(int n)
{
    Func<int, int> nthFactorial = default(Func<int, int>);

    nthFactorial = number => number < 2
        ? 1
        : number * nthFactorial(number - 1);

    return nthFactorial(n);
}
```

### Անվանակոչում

[Naming](#https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/local-functions#naming)

**Լոկալ ֆունկցիաները** մեթոդների նման ունեն անվանվում: **Lambda** արտահայտությունները անանուն մեթոդներ են և պետք է վերագրվեն `delegate` տիպի փոփոխականների, որոնք սովորաբար կամ `Action` կամ `Func` տեսակներ են։ Երբ դուք հայտարարում եք լոկալ ֆունկցիա, գործընթացը նման է սովորական մեթոդ գրելուն. հայտարարվում է վերադարձի տեսակը և ֆունկցիայի ստորագրությունը։

### Բացահայտ վերագրում

[Definite assignment](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/local-functions#definite-assignment)

**Լամբդա արտահայտությունները** օբյեկտներ են, որոնք հայտարարվում և նշանակվում են կատարման ժամանակ։ Որպեսզի լամբդա արտահայտությունն օգտագործվի, այն պետք է անպայման վերագրվին `Action/Func` տիպի փոփոխականի։ Ուշադրություն դարձրեք, որ `LambdaFactorial`-ը պետք է հայտարարի և ինիցիալիզացնի `nthFactorial` լամբդա արտահայտությունը սահմանելուց առաջ։ Դա չանելը կառաջացնի կոմպիլյացիայի սխալ։

**Լոկալ ֆունկցիաները** սահմանվում են կոմպիլյացիայի ժամանակ։ Քանի որ դրանք չեն նշանակվում փոփոխականների, դրանց հնարաովոր է կանչել կոդի ցանկացած տեղից: `LocalFunctionFactorial`-ում, դուք կարող եք հայտարարել լոկալ ֆունկցիան `return` հրամանից առաջ կամ հետո։

### Variable capture

[Variable capture](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/local-functions#variable-capture)

Դիտարկենք հետևյալ օրինակը՝

```c#
int M()
{
    int y;
    LocalFunction();
    return y;

    void LocalFunction() => y = 0;
}
```

Քանի որ `LocalFunction`-ը կանչվում է `return` հրամանից առաջ, y-ը անպայմանորեն վերագրված կլինի մինչև `return` հրամանը։
