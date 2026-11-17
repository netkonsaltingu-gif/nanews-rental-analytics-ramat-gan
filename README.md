# nanews-rental-analytics-ramat-gan
 How We Built NAnews | Market Analytics: From Scattered Rental Listings to a Data-Driven Housing Research System in Israel

# How We Built NAnews | Market Analytics: From Scattered Rental Listings to a Data-Driven Housing Research System in Israel

In November 2026, our rental market analysis for Ramat Gan recorded 92 apartment advertisements. But only 77 contained usable rental prices, and just 49 provided enough information to calculate rent per square metre.

That difference — 92, 77 and 49 — illustrates why we decided that collecting apartment advertisements was not enough. We needed to build a system capable of distinguishing available information from missing data, calculating statistics correctly and explaining what the numbers actually mean.

The result was **NAnews | Market Analytics**, a project developed within the Israeli news platform NAnews – Nikk.Agency.

Our objective was straightforward: turn fragmented rental advertisements from different online sources into structured, comparable and regularly updated market research covering Israeli cities.

The technical work behind that idea proved considerably more complicated than producing a table of average prices.

We needed to solve problems involving collection, duplicates, city identification, incomplete advertisements, multilingual publishing, historical data, WordPress integration and the distinction between a genuine market change and a change in the composition of the collected sample.

Ramat Gan became one of the cities through which we could demonstrate how the system works.

## The first challenge: advertisements were not designed for statistical analysis

An apartment advertisement is written to attract a tenant, not to populate a research database.

One owner writes that an apartment is "large and renovated" but does not provide its area. Another includes the number of rooms but omits the monthly rent. A third places important details inside a long description rather than in separate fields.

Even the city name cannot always be trusted when it appears in a website category.

A listing might be placed in a broader metropolitan section while the property itself belongs to a neighbouring municipality.

We therefore had to distinguish the information supplied by the source from the structured information needed by our system.

Our working model focused on the essential characteristics of a rental advertisement: its source, city, asking price, number of rooms, floor area, location, description and observation date.

Missing information had to remain missing.

If an advertisement did not contain a reliable price, the system could still retain the listing, but it should not invent a monthly payment or include a zero in the calculation of average rent.

The same principle applied to floor area and room count.

This became one of the foundations of NAnews | Market Analytics: the software should organise available facts, not manufacture missing ones.

## Two websites, different responsibilities

We organised the project around two connected WordPress environments.

The first, advertising.nikk.agency, became the working environment for collection, preparation and analysis.

The second, nikk.agency, served as the public publishing platform for the research.

Separating those responsibilities was important.

The analytical environment needed tools for working with sources, checking collected advertisements, managing city data, calculating statistics and preparing multilingual content.

The public website needed reliable, readable articles that could be updated without recreating the entire research process.

Several WordPress components were developed around that division of responsibilities.

**SEO Content Monitor** handled the source-management and collection side of the rental project.

**Rentals Template** handled analytical presentation, multilingual publication preparation and the generation of research pages.

**NAnews Market Analytics**, on the publication side, received the prepared materials and managed their presentation on the public news website.

Rather than turning the public website into a complex collection platform, we kept the analytical workflow separate from the reader-facing pages.

This allowed the same research framework to support both individual city reports and a national overview.

## Why we chose controlled collection instead of an uncontrolled crawler

Our work began with selecting and testing the sources.

We deliberately avoided treating every large real-estate portal as an acceptable source.

For this project, we excluded Yad2, Madlan, Zipika and ad.co.il from the collection workflow. We instead focused on other public listings, local agencies, private advertisements and selected community sources.

Realta was among the sources designated for review, and Telegram sources required a separate approach to checking available posts.

The central principle was to examine sources individually rather than launch an unrestricted search across the entire internet.

We added a source, tested the results and examined what the system extracted before deciding whether it should become part of the wider collection process.

This approach made errors easier to identify.

If a source repeatedly omitted prices or returned properties for sale instead of rental apartments, we could investigate the problem without contaminating an entire city dataset.

We also needed a consistent rule for duplicate sources.

Different pages belonging to the same website should not automatically be counted as independent sources merely because their URLs were different.

At the listing level, the system had to avoid processing the same advertisement repeatedly.

These controls reduced unnecessary processing and helped prevent duplicated apartments from distorting the market statistics.

## Normalising prices without inventing information

Price extraction became a particularly important part of development.

Israeli rental advertisements contain several kinds of monetary information. Alongside monthly rent, a description may mention municipal tax, building maintenance charges, deposits or utility payments.

Those amounts must not be confused.

For our apartment-rental research, we established an analytical range of **₪1,800 to ₪9,000 per month**, inclusive.

Listings outside that range do not enter the main rental-price calculations.

This is a project-specific analytical filter, not a claim that no apartments exist below or above those amounts.

We also had to preserve the distinction between a missing price and a price that exists but is outside the permitted range.

The first is incomplete information. The second is information excluded under an explicit research rule.

That difference matters when explaining why the total number of collected advertisements is larger than the number used to calculate the average.

The same discipline applied to floor area.

Only listings with both a usable monthly rent and a usable area could contribute to the square-metre calculation.

It was not acceptable to estimate an apartment's size from the number of rooms or assume that a missing field had a typical value.

## Ramat Gan: the results of that approach

The [NAnews rental market study for Ramat Gan](https://nikk.agency/he/nanews-rental-7-17-he/) provides a practical example of how the system turns collected advertisements into a public research report.

The November 17, 2026 snapshot contained:

- **92 advertisements** in the saved sample.
- **77 advertisements** with prices suitable for calculation.
- **49 advertisements** with both price and floor-area information.
- **₪5,743** average advertised monthly rent.
- **₪5,650** median advertised monthly rent.
- **₪82.9** average monthly asking rent per square metre.

The difference between these three sample sizes is essential.

The system should not divide the sum of 77 known rental prices by all 92 advertisements.

Nor should it report the square-metre figure as if every listing contained a reliable area.

Each statistic has its own valid denominator.

For readers, this may appear to be a small methodological detail. For developers, it is one of the distinctions that determine whether an analytical result is trustworthy.

## How we handled average rent and median rent

A simple average can be calculated by adding the eligible prices and dividing by the number of those prices.

But we did not want the entire study to depend on that one number.

Expensive apartments can raise the mean even when most of the available offers remain below it.

That is why we included the median alongside the average.

The median identifies the central position of the sorted price distribution.

On November 17, Ramat Gan's average asking rent was ₪5,743, while the median was ₪5,650.

The difference was relatively modest, but the two indicators still described different characteristics of the sample.

We also added calculations by room count.

The same Ramat Gan snapshot recorded an average of ₪4,308 for two-room apartments, ₪6,476 for three-room properties and ₪6,980 for four-room apartments.

Those categories were based on different groups of observations.

They should not be interpreted as the price of adding an extra room to the same apartment.

The purpose was to give readers a more relevant reference point for their own housing requirements.

## The square-metre calculation required another decision

There is more than one way to produce a figure described as the average rental price per square metre.

One method divides the total rent across a set of apartments by their combined floor area.

Another calculates the rent per square metre for every eligible apartment and then averages those individual ratios.

Our research uses the second approach.

This distinction matters because large apartments otherwise receive greater influence in an area-weighted calculation.

Consider two hypothetical properties.

The first costs ₪6,000 a month and measures 50 square metres. Its asking rent is ₪120 per square metre.

The second also costs ₪6,000 but measures 100 square metres. Its asking rent is ₪60 per square metre.

The average of those two individual ratios is ₪90 per square metre.

Dividing their combined rent by their combined area produces ₪80 instead.

Both are mathematically valid calculations, but they answer different statistical questions.

We needed the project's methodology to remain consistent rather than silently alternate between methods.

For Ramat Gan, the published result was ₪82.9 per square metre, calculated from 49 suitable advertisements.

## Making the system work in Russian and Hebrew

The project was intended for an Israeli readership that does not use only one language.

That meant preparing public research pages in Russian and Hebrew.

The task involved more than translating article headings.

Rental advertisements often contain Hebrew street names, local terms, abbreviations and descriptions mixing several languages.

Our workflow needed to preserve numerical facts while preparing separate language versions of the relevant text.

The asking price, floor area and room count should remain the same regardless of whether a reader opens the Russian or Hebrew report.

We also established limits for listing descriptions so that the public pages would remain readable.

Brief descriptions had to preserve meaningful property details without reproducing unnecessary promotional material, contact information or irrelevant text.

Another important decision concerned previously processed translations.

When a listing had already been prepared in a required language, repeating the same translation work was unnecessary.

The project therefore used existing saved language versions where available and focused translation work on missing outputs.

This helped keep the multilingual process more consistent and avoided unnecessary repeated processing.

The Hebrew interface also required attention to right-to-left presentation, while Russian content retained its normal left-to-right layout.

The analytical figures remained shared, but their presentation had to work naturally in both languages.

## Building a history without inventing market trends

Collecting a new dataset creates another problem: readers naturally want to know whether prices have increased or decreased.

But a change in the average of two datasets does not automatically represent a change in the price of comparable apartments.

The Ramat Gan research makes this particularly clear.

On November 8, the system recorded 98 advertisements with an average asking rent of ₪5,667 and a median of ₪5,800.

On November 17, the saved sample contained 92 advertisements.

The average had increased to ₪5,743, while the median had declined to ₪5,650.

The square-metre figure moved from ₪75.6 to ₪82.9.

These changes did not all point in the same direction.

The project therefore needed a way to preserve dated observations and explain them without claiming that every landlord had changed the rent.

Our analytical pages present changes in the collected sample.

They do not describe those changes as a verified index of completed rental transactions.

We also worked on maintaining continuous historical presentation so that the charts remained understandable when a calendar day did not produce a genuinely new collection.

The objective was to preserve a readable timeline without inventing fresh observations.

The distinction between a source-update date and the date on which an analytical report is generated also matters.

A newly generated article does not necessarily mean that every advertisement within it was first published that day.

## Comparing Ramat Gan with other Israeli cities

City research becomes more useful when readers can understand how the results fit into a wider market.

The [national Israeli rental market analysis](https://nikk.agency/he/apartment-rentals-israel/) published on November 17 covered 2,681 advertisements from 53 cities.

Of these, 2,128 had usable rental prices.

The national average asking rent was ₪4,734 per month, the median was ₪4,500, and the average price per square metre was ₪61.4, based on 1,624 observations.

Ramat Gan's monthly average exceeded the national figure by ₪1,009.

But the national dataset included cities with different property types and different numbers of advertisements.

A useful comparison therefore also requires looking at neighbouring municipalities.

In [Givatayim](https://nikk.agency/he/nanews-rental-7-18-he/), the national snapshot recorded 22 advertisements, with an average asking rent of ₪6,830, a median of ₪6,900 and a square-metre figure of ₪90.6.

In [Tel Aviv–Yafo](https://nikk.agency/he/nanews-rental-7-7-he/), 158 advertisements produced an average of ₪6,327, a median of ₪6,350 and a square-metre figure of ₪104.3.

Kiryat Ono recorded 42 advertisements, with an average rent of ₪6,627, a median of ₪6,750 and a square-metre price of ₪72.6.

Or Yehuda had 58 advertisements, with an average of ₪6,404, a median of ₪6,500 and an average price of ₪77.7 per square metre.

Meanwhile, [Petah Tikva](https://nikk.agency/he/nanews-rental-7-14-he/) recorded 106 advertisements, with an average of ₪5,548, a median of ₪5,300 and a square-metre figure of ₪72.9.

These comparisons illustrate why an apartment's total monthly rent and its cost per square metre must be evaluated together.

They also show the importance of identifying which cities belong in the relevant comparison rather than automatically comparing every location with Tel Aviv.

## Why the local economy matters to housing research

Ramat Gan is not simply a residential city next to Tel Aviv.

Its Diamond Exchange district is an important commercial centre associated with international business, financial services and the jewellery industry.

That economic environment matters to people deciding where to live because employment locations influence commuting patterns and the practical value of residential addresses.

NAnews examined one international dimension of this activity in its [investigation into Israeli ownership connections in Ukraine's jewellery industry](https://nikk.agency/en/jewelry-business-in-ukraine-israel/).

The investigation analysed Ukrainian companies with Israeli ownership connections and identified declared business relationships involving the Israel Diamond Exchange.

Those findings do not demonstrate that the jewellery industry is responsible for Ramat Gan's rental prices.

They do, however, illustrate the wider economic environment in which the city's residential market operates.

A person working near the Diamond Exchange may value an apartment within walking distance of the office.

Another household may prioritise schools, family connections or access to the light rail.

Rental statistics become more useful when they are presented alongside the practical realities of the city.

## Connecting data analysis with government information

The development of our system also raised an editorial question.

What should a reader do after discovering that a city is expensive?

For some people, the next step is to compare a nearby municipality or reduce the required apartment size.

Others may need to understand whether they qualify for government rental assistance.

Israel's Ministry of Aliyah and Integration provides [official information about rental assistance for eligible new immigrants](https://www.gov.il/en/pages/rental-assistance-for-olim?chapterIndex=2).

Eligibility depends on the applicable programme rules and personal circumstances.

The existence of a rental advertisement or a high average city rent does not establish entitlement.

Our analytical software does not determine eligibility. Its purpose is to measure and explain recorded asking prices.

Government resources provide a different type of information, and linking to them in the appropriate context helps readers distinguish market data from public assistance programmes.

## The publishing layer was as important as the calculations

A statistical result is useful only if readers can access and understand it.

That required us to develop a publication workflow rather than stop at generating figures inside the analytical environment.

The prepared research needed to reach the public NAnews website with its city identity, language version, statistical indicators and explanatory content intact.

We worked on preserving stable public pages so that updated studies could refresh existing material instead of creating unnecessary duplicate URLs.

The publication system also needed search-engine metadata suitable for Russian and Hebrew readers.

A research page about Ramat Gan should clearly identify the city, its current observation period and the relevant housing statistics.

This is different from publishing a generic article entitled "Apartment Rental Prices in Israel" every time the underlying dataset changes.

The city pages were designed to function as continuing analytical resources.

The national page provided a broader comparison across the cities included in the research.

We also separated the internal analytical history from the public presentation.

Historical observations were retained in the analytical environment, while the publishing system received the prepared content and relevant snapshot information.

This division reduced the need to reconstruct the entire collection process on the public website.

## What we learned while developing the project

Several lessons emerged from the development work.

First, data quality matters more than the number of collected advertisements.

A dataset containing 100 incomplete listings may be less useful for pricing research than a smaller group with clearly established prices and areas.

Second, a missing field is not a reason to invent a plausible value.

Third, identifying the correct city is part of the analytical process, not merely a cosmetic label attached to the finished article.

Fourth, multilingual publication requires consistency between language versions, particularly when the same price and property characteristics appear in both.

Fifth, historical statistics must retain the distinction between changes in observations and changes in actual market prices.

And finally, a working analytics project needs both a data-processing system and an editorial publishing layer.

A database can calculate a median. It cannot, by that calculation alone, explain to a family why an apartment without a lift may be unsuitable or why a short-term lease creates additional costs.

That interpretation belongs in the published research.

## Why we are explaining the development process on GitHub

The [NAnews profile on GitHub](https://github.com/netkonsaltingu-gif) provides an appropriate place to discuss the technical thinking behind projects that connect information collection, software development and journalism.

This article describes the working approach behind NAnews | Market Analytics. It is not a claim that the private production plugins, database or collection infrastructure have been released as open-source software.

The development process involved practical decisions about source management, duplicate prevention, validation, statistical calculations, historical observations, multilingual presentation and WordPress publication.

Ramat Gan provides a concrete example of the outcome.

Its November 17 research contains 92 advertisements, but only 77 usable rental prices and 49 observations suitable for calculating the cost per square metre.

Those three numbers explain much of the engineering challenge.

The software needed to preserve the difference between collected information and information suitable for a specific calculation.

Without that discipline, the final figures could look convincing while conveying a misleading picture of the market.

## From apartment advertisements to transparent research

NAnews | Market Analytics began with a simple practical problem: people searching for housing in Israel encounter prices scattered across many sources, presented in different formats and with varying levels of detail.

We developed a workflow to bring those observations into a common analytical structure.

That work required decisions about which sources to use, how to handle incomplete listings, how to preserve city identity, how to calculate reliable statistics and how to publish the resulting research in Russian and Hebrew.

The Ramat Gan study demonstrates the result.

Readers can see not just an average asking rent, but also a median, room-based comparisons, price segments, square-metre calculations and a dated history of the collected sample.

The system cannot replace inspecting an apartment, negotiating a lease or checking the actual condition of a building.

It also cannot turn asking prices into verified transaction prices.

What it can do is make the information more structured, more comparable and easier to evaluate.

For us, that is the purpose of combining software development with journalism: not merely collecting more information, but helping readers understand what the available information can — and cannot — tell them.

---

*Methodology and project note: The Ramat Gan figures in this article refer to the NAnews | Market Analytics research snapshot dated November 17, 2026. The nationwide and neighbouring-city comparisons use the consolidated research for that date. Rental figures describe advertised asking prices, not completed transactions. The technical discussion describes the development workflow and established project components, not a public release of the private WordPress source code.*
