# Вежбе -- Шести час -- Додавање навигације и корпе

[повратак](../../README.md)

**Наставак унапређивања и додавања нових функционалности интернет продавници.**

**Задатак:** Додатни навигацију, односно мени са категоријама. Потом омогућити кориснику да додаје производе у корпу.

## Додавање навигације:

### Почетни кораци

- У _SpisakProizvodaViewModel_ додати _TrenutnaKategorija_
- Изменити метод _Spisak_ који сада филтрира производе и према категорији (у методи додати још једно поље _trenutnaKategorija_)
- Покренути и пробати `https://localhost:5001/Proizvod/?trenutnaKategorija=racunar`
- Потом променити изглед рута у `Startup.cs`:
	- увек се прво наводи најдужа рута (у нашем примеру то је рута облика `../kategroija/stranaBr`, нпр. `https://localhost:5001/Proizvod/racunar/Strana2`)
	- на крају се наводи најопштија могућа рута
	- погледати коментаре у коду у `Startup.cs`
	- више о рута у [документацији](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-3.0)

### Коришћење _ViewComponent_ ради додавања навигације

- Више о _ViewComponent_, као и разни примери могу се видети у [документацији](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/view-components?view=aspnetcore-3.0).
- Направити фолдер _Components_, а у њему _NavigacijaViewComponent_
- Додати метод _Invoke_
- Креирати _Razor_ страницу за приказ комоненте: `Views/Shared/Components/Navigacija/Default.cshtml`. Називи су битни и путања мора да изгледа овако. (подразумеване путање се могу променити у конфигурацији)
- У _\_Layout.cshtml_ позвати комоненту са _@await_
- Обележавање тренутне категорије у навигацији: компоненти је (поред низа категорија) неопходно проследити и тренутну категорију. Направити _NavigacijaViewModel_ и изменити _Invoke_.


## Додавање информација везаних за одређено подручје 

Додати класу (прецизније екстензију) _Cultures_ (може се ставити у фолдер _Infrastructure_) и додати потребна подешавања за српско говорно подручје. Користи се приликом исписа цена (на пример, у _ProizvodIspis.cshtml_)

## Креирање корпе

- Креирати класу _Models/Korpa.cs_
- Изменити _ProizvodIspis.cshtml_: додати дугме за додавање производа у корпу и поље за одабир количине (креирати форму)
- Тренутна корпа се не чува у бази. Тек када корисник заврши куповину, корпу чувамо у бази (на неком наредном часу, у виду поруџбина). За сада корпу чувамо преко сесија. Сваки корисник има своју сесију (па је самим тим лако одржавати стање да сваки корисник има своју корпу).
- У `Startup.cs` додати: `services.AddMemoryCache()`, `services.AddSession()` и `app.UseSession()` (омогућава чување у меморији и да се захтеви који долазе клијента аутоматски вежу за сесије)
- Креирати `Infrastructure/SessionExtension`
- Креирати `Controllers/KorpaController`
- Креирати `View/Korpa/SpisakKorpe.cshtml`

[повратак](../../README.md)