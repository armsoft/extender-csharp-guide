# if, switch արտահայտություններ և ցիկլեր

## Բովանդակություն

- [if, switch արտահայտություններ և ցիկլեր](#if-switch-արտահայտություններ-և-ցիկլեր)
  - [Բովանդակություն](#բովանդակություն)
  - [If արտահայտություններ](#if-արտահայտություններ)
  - [Switch արտահայտություն](#switch-արտահայտություն)
  - [Ցիկլեր](#ցիկլեր)
    - [while do ... while ցիկլեր](#while-do--while-ցիկլեր)
    - [For ցիկլեր](#for-ցիկլեր)

## If արտահայտություններ

if, if-else, արտահայտությունների միջոցով որոշվում է ծրագրի կատարման ճյուղը կախված if արտահայտության բուլեան արժեքից։

```c#
int tempInCelsius = 19;

    if (tempInCelsius < 20) // արտահայտության արժեքը կլինի true
    {
        Console.WriteLine("Cold.");  // կկատարվի այս տողը
    }
    else
    {
        Console.WriteLine("Perfect!"); // այս ճյուղը կանտեսվի
    }
```

**else** ճյուղը պարտադիր չէ։

Եթե տվյալ ճյուղը պարունակում է մեկ տող ձևավոր փակագծերը պարտադիր չեն։

```c#
    int value = -50;

    if (value < 0 || value > 100) // ստուգվում է արդյոք value -ի արժեքը փոքր է 0 կամ մեծ 100-ից։
        Console.Write("Warning: not acceptable value! "); // այս տողը չի կատարվի 

```

**else if** արտահայտությունները օգտագործվում են նախնական if պայմանից հետո լրացուցիչ պայմաններ փորձարկելու համար: Սա թույլ է տալիս հաջորդաբար ստուգել մի քանի պայման: Կկատարվի առաջին իսկ **else if** ճյուղը, որի պայմանը կլինի true: Եթե բոլոր պայմանները լինեն false կկատարվի **else** ճյուղը նրա առկայության դեպքում:

```c#
  decimal bonus, salary, performance;

  performance = 2m;

  salary = 1_000_000m;

  if (performance == 1m)
      bonus = salary * 0.1m;
  else if (performance == 2m)
      bonus = salary * 0.09m; // կկատարվի այս ճյուղը
  else if (performance == 3m)
      bonus = salary * 0.07m;
  else
      bonus = 0;
```

[The if statement](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/selection-statements#the-if-statement)

## Switch արտահայտություն

**switch** արտահայտությունը, ինչպես և **if** -ը օգտագործվում է, պայմանանից կախված, նկարագրված ճյուղերից մեկը կատարելու համար: Կատարման ժամանակ switch արտահայտությունը հաշվարկվում է մեկ անգամ, այնուհետև կատարվում է պայմանի համեմատում ամեն դեպքի համար։ Պայմանը բավարարված լինելու դեպքում կկատարվի համապատասխան ճյուղը։

**break** հիմնաբառը օգտագործվում է **switch** բլոկից դուրս գալու համար։ Նրա բացակայության դեպքում ընթացիկ ճյուղը կատարելուց հետո կկատարվի հաջորդող նկարագրված դեպքերի (**case**) մշակում։  

**default** հիմնաբառը պարտադիր չէ և սահմանում է այն ճյուղը, որը պետք է կատարվի երբ որևէ ճյուղի պայման բավարարված չէ:

```c#
int day = 4;
switch (day) 
{
  case 6:
    Console.WriteLine("Today is Saturday.");
    break;
  case 7:
    Console.WriteLine("Today is Sunday.");
    break;
  default:
    Console.WriteLine("Looking forward to the Weekend.");
    break;
}

```

```c#
  int today = 6;
  string tomorow;

  switch (today + 1)
  {
      case 1:
          tomorow = "Monday";
          break;
      case 2:
          tomorow = "Tuesday";
          break;
      case 3:
          tomorow = "Wednesday";
          break;
      case 4:
          tomorow = "Thursday";
          break;
      case 5:
          tomorow = "Friday";
          break;
      case > 5:
          tomorow = "Weekend";
          break;
      default:
          tomorow = "Unknown";
          break;
  }

```

[The switch statement](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/selection-statements#the-switch-statement)

## Ցիկլեր

Մեկ այլ կարևոր կոնցեպտ է ցիկլերը: Ցիկլերը օգտագործվում են այն դեպքում երբ անհրաժեշտ է կրկնել որոշակի կոդի բլոկ
մեկից ավել անգամ։

[Use loops to repeat operations](https://learn.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/tutorials/branches-and-loops#use-loops-to-repeat-operations)

### while do ... while ցիկլեր

while արտահայտությունը շարունակաբար ստուգում է պայմանը և կատարում նրան հաջորդող կոդի բլոկը քանի դեռ պայմանը կատարվում է:

```c#
int counter = 0;
while (counter < 10) // հաջորդող բլոկը կկատարվի 10 անգամ մինչև counter փոփոխականի արժեքը դառնա 10
{
    Console.WriteLine($"Hello World! The counter is {counter}");
    counter++; // 1-ով ավելացնում է counter փոփոխականի արժեքը 
}

```

while ցիկլը ստուգում է պայմանը մինչ հաջորդող բլոկի կատարելը: Do ... while ցիկլի դեպքում սկզբում կատարում է բլոկը, այնուհետև ստուգում է պայմանը:

```c#
int counter = 0;
do
{
    Console.WriteLine($"Hello World! The counter is {counter}");
    counter++;
} while (counter < 10);

```

### For ցիկլեր

Մեկ այլ ֆիկլի տեսակ է հանդիսանում **for** ցիկլերը։

```c#
for (int counter = 0; counter < 10; counter++)
{
    Console.WriteLine($"Hello World! The counter is {counter}");
}

```

Վերևում բերված **for** ցիկլը կատարում է նույն աշխատանքը, ինչ և **do** ցիկլը: Ցիկլի **for** արտահայտությունը ունի երեք մաս։

1. Առաջին մասը **for**-ի սկզբնավորիչն է  **int counter = 0;**, որը հայտարարում է **counter** ցիկլի փոփոխականը և սահմանում է նրա արժեքը 0:
2. Հաջորդը (**counter < 10;**) **for** ցիկլի պայման է, որի կատարման դեպքում այն շարունակելու է աշխատել։
3. Վերջում սահմանվում է թե ինչպես է փոխվելու ցիկլի փոփոխականը հերթական պտույտից հետո։ **counter++** տվյալ դեպքում այն կավելացվի մեկով։
