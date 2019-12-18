# Econ 134 Lecture Notes
By: Alan Liang, Zishen Liu, Umar Maniku, Youmna Rabie

## I. Key macro statistics: GDP, Inflation
### a. Underlying data, concepts
- GDP: market value of all final goods & services newly produced during a time period
    - GDP is not a good measure of welfare:
        - Doesn't count quality of life factors
        - Only counts market as opposed to non-market activity
        - Externalities are not measured
            - Negative externalities from "production" associated with wars is included, even if the "goods" are harmful to society
            - Goods with positive externalities such as government services and healthcare measured primarily by its costs
        - Difficulties measuring new goods
- Approaches to measuring GDP
    - Income: total income from factors of production (land, labor, capital)
    - Expenditure ($Y = C + I + G + NX$)
    - Value at Production: market value of all newly produced final goods and services
- Inflation = $\frac{P_{new} - P_{old}} {P_{old}}$
- Real GDP: GDP at "constant prices", net of inflation
- Price indexes: PPI, CPI, GDP Deflator, PCE (personal consumption expenditure) Deflator, core CPI
    - CPI: index that measures price basket of goods & services bought by a typical urban household
    - PCE deflator: $\frac{\text{Nominal PCE}}{\text{Real PCE}}$
    - GDP deflator: $\frac{\text{Nominal GDP}}{\text{Real GDP}}$
- Price indexes important because:
    - Measure "real wages"
    - Used to measure cost of living changes
    - To calculate wages indexed to inflation
    - Monetary policy
- Cost of living index (COLI): Cost of achieving the same utility over time in the cheapest way possible (potentially changing the basket)
    - Removes substitution bias
- Cost of goods index (COGI): The cost of a fixed basket of goods over time (can use Laspeyres, Paasche, or Fisher index to compute depending on how quantity is fixed)
- Data we need:
    - What people buy in order to construct basket: BLS Consumer Expenditure Survey
    - Price for identical items over time to measure price changes

### b. Alternative price indexes and conceptual differences- Laspeyres, Paasche, Fisher

- Laspeyres fixes basket at initial period w/ initial quantities as weights to the price ratios: $\frac{p_{a2}q_{a1} + p_{b2}q_{b1}}{p_{a1}q_{a1} + p_{b1}q_{b1}} = q_{a1} \frac{p_{a2}}{p_{a1}} + q_{b1} \frac{p_{b2}}{p_{b1}}$ 
    - US CPI is a Laspeyres price index as there is no need for updated quantities, reducing data burden
    - Encounters substitution bias
    - Grows faster than COLI
- Paasche fixes basket at final period w/ final quantities as weights to the price ratios: $\frac{p_{a2}q_{a2} + p_{b2}q_{b2}}{p_{a1}q_{a2} + p_{b1}q_{b2}} = q_{a2} \frac{p_{a2}}{p_{a1}} + q_{b2} \frac{p_{b2}}{p_{b1}}$
    - Downward bias (understates inflation)
- Fisher: $\sqrt{\Delta P_L \times \Delta P_P}$
    - US GDP uses chained Fisher index
- If income is normalized to $100 in year 1, then change in price of basket is inflation
- For quantity indexes, use initial/final period prices as weights
- Laspeyres price index = Paasche quantity index 
- Paasche price index = Laspeyres quantity index
- Fisher price index = Fisher quantity index

### c. Key measurement challenges- New goods bias, substitution bias

- Substitution bias: people change preferences and substitute to cheaper goods from year 1 to year 2, no matter if there is inflation or deflation.
    - The Laspeyres index does not capture this as it retains the year 1 basket quantities, making it upward biased.
    - Paasche over-accounts for substitution bias by using quantities after people have substituted to account for price changes.
- New goods: did not exist before so no comparison possible as no old price/quantity exists
    - How to quantify quality improvements: computers have become more functional over time
- Solutions to new/improved goods
    - "Linking in": replace an old good with a new good by having both goods' prices recorded in the middle year
    - "Chaining": reset base year every year, then chain the price level changes year over year
    - Hedonics: measure change in quality or in terms of chracteristics of new good (lumens per $)
- New goods bias: product improvements are not counted, hence overstating the prices of the same goods in future periods. Generally, prices increase but when accounting for product improvement, price actually decreases. 
    - Hence, inflation is overstated and growth is understated.
    - Standard price indexes "link in"  new goods and thus miss the effective price reductions (due to increases in quality) associated with new goods

### d. Cross-country comparisons using PPP adjustments, and measurement challenges

- Challenge: For developing countries, PPP adjusted measures of GDP tend to be higher than standard market-based measures
    - $80 in China can buy more stuff than $100 in USA, thus PPP is higher than when you just simply convert according to market exchange rates
    - Due to non-traded goods
- PPP adjusted comparisons: convert each country's GDP into USD using market exchange rate, then divide by the country's PPP index
    - PPP index is a price level ratio between the domestic country and the US. The PPP index value will be lower for countries where things are cheaper
    - Calculated using the cost of constant "basket" in different countries, then finding the ratio relative to the US basket. 
- Another problem: how do you price a "basket" of goods in different countries? What if you can't find the whole basket in some countries?

## II. Regressions
### a. OLS regression- interpretation of coefficients, standard errors

- Single variable regression: Coefficient estimate $\beta$ implies that an additional unit of the regressor is associated with an increase of $\beta$ in the dependent variable
- Taking the log of both sides converts coefficients to percent changes
- Standard errors give a sense of how much variation in estimates would arise just by chance, and is used to reject the null hypothesis
- Does not show a causational relationship!
    - Reverse causality: causation actually occurs the other way around (Y causes X)


### b. Omitted variable bias, reverse causality

- Omitted variables: output variable cannot solely be explained by X, but also by other factors as well
- If variables in the regression (regressors) are correlated with the error term, then the coefficient estimate will be a biased estimate of the regressor's effect on the dependent variable
    - If the correlation is positive and both the error and regressor correlate with Y in the same direction, then the effect is overstated (in magnitude)
    - If the correlation is positive and the error and regressor correlate with Y in different directions, then the effect is understated (in magnitude)
    - If the correlation is negative and the error and regressor correlate with Y in the same direction, then the effect is understated (in magnitude)
    - If the correlation is negative and the error and regressor correlate with Y in different directions, then the effect is overstated (in magnitude)
    - Regressors need to be uncorrelated with error term

### c. Multiple regression and controls

- Multivariable regression: Each coefficient gives change in predicted $y_i$ for a change in one particular regressor holding other regressors fixed
- If we were successful in controlling for other regressors, then we would have a causal relationship
- Can be used to control for confounding factors
- Randomized experiments eliminates possibility of omitted variable bias because it operates under the assumption that everything is equal (on average) between the two groups aside from the treatment

### d. Natural experiment, IV regression

- Natural experiment: situtations where people assigned to treatment or control was as if random
- IV regressions often arise from natural experiments
- Two requirements for a good instrument Z:
    - Relevance: Correlated with the RHS variable (regressor)
    - Exogeneity: Not correlated with the error term (any other omitted variable)
- Using an instrument eliminates problem of systematic correlation between omitted variable and regressor because randomness essentially guarantees that the fitted values are independent of the error term
    - All variance in X (regressor) is due to Z (instrument)
- Implement IV regression through 2SLS:
    - Regress RHS variable on instrument to get fitted values
    - Run a regression of LHS variable using fitted values
    - The coefficient on the fitted value regressor is a good estimate of the causal effect of the regressor on the LHS variable
    - Because X may be correlated with the error term, if we have an instrument that satisfies the exogeneity and relevance condition to fit X, the fitted X's variance is solely due to the instrument and hence when we regress Y onto the fitted X, we observe the direct effect of X without omitted variables on Y. 

### e. Confidence intervals, t-statistics, p-values, R-squared, dummy variables

- Confidence interval gives range of values where true relationship coefficient would exist
- If CI does not contain 0 --> statistically significant
- t-statistic = $\frac{\hat \beta}{SE(\hat \beta)}$
    - If $\text{t-stat} \in (-2, 2)$ then coefficient is statistically insignificant
- Statistically significant coefficient does not imply large effect  (economic significance), depends on size of coefficient
- P-value: Probability that the coefficient estimate is observed if the true $\beta = 0$
    - A tiny p-value suggests that the coefficient estimate is statistically different from 0
-  $R^2$: Gives a measure of the fraction of the total variation in LHS variable explained by the explanatory variables in the regression. Essentially, how well does the model "explain" the data?
    -  $R^2$ can be low even if all coefficients are statistically significant because the data is very noisy
- Dummy variables: Variables that take a value of zero or one between two or more categories
    - The difference in dummy variable coefficients show the average differences in effect (measured through LHS variable) of 2 different dummy variable states

## III. Money
### a. Properties of Money

- Store of value: hold money in order to buy something later
- Medium of exchange: pay for things with money
- Unit of account: quote prices, wages in terms of units of money
- If money didn't exist, then the world economy would be a barter system requiring a double coincidence of wants
- Monetary base: coins and bills, deposits of banks at Federal Reserve
- M1: Monetary base + coins and bills outside of Federal reserve + checkings accounts
    - Measure of money's function as a medium of exchange
- M2: M1 + savings accounts and some money market funds, time deposit funds
    - Measure of money's function as a store of value

### b. Money demand and money supply, implications for interest rates

- Demand for money is related to its function: portfolio choice problem, acceptance in stores, "stable" unit in which to post prices
- Many assets pay positive returns that rise with the interest rate
    - Thus, a higher nominal interest rate implies a higher opportunity cost of holding money, lowering its demand
    - Money demand has a negative relationship with the nominal interest rate
- Nominal quantity of money supplied in an economy is fixed by the Central Bank --> vertical line where money supply is fixed
    - MS only shifts due to open market operations: QE or Fed changing its balance sheet
- MD shocks:
    - Increase in GDP: more money needed to fund transactions (Christmas = $\uparrow$ MD)
    - Financial innovation: less money needed for transactions (credit cards = $\downarrow$ MD)
- Useful simplification: movement of FFR passes onto other interest rates like the treasury bill or mortgage rate
    - These are riskier, longer-term assets with a positive interest rate spread but they comove with the FFR
- Milton Friedman's Monetarism: Fed should conduct policy such that money growth is constant. This should eliminate any monetary surprises.
    - $MV = PY \iff g_M + g_V = \pi + g_Y$
        - M: money supply
        - V: velocity of money
        - P: price level
        - Y: real output
    - If velocity of money is stable, then stabilizing $g_M$ will stabilize $\pi + g_Y$
        - This is a bad assumption: V is dependent on interest rates!
    - 1960-1979: Friedman saw that US log velocity of M1 was growing at a steady rate, implying that $g_V$ was constant
    - After 1979: velocity becomes unstable. If the monetarist approach was followed, this would have led to massive fluctuations in output and prices

## IV. Great Depression

### a. Before the Great Depression (1920s)

- Real GDP growth from 1919-1929 fluctuated significantly
    - Recession in 1921
    - Inflation hovered around 0 except in 1921 when it was -15%
- Stock prices increased greatly
- Active academic literature on whether booms sow the seeds for later busts
- Contributors to collapse: stock market crash, banking panics, monetary/fiscal policy

### b. Great Depression

- Initially caused by stock market crash (black Tuesday) and declines in industrial production
- Banking panics occurred 4 times between 1930-1933
    - Each caused hundreds of banks to be suspended
    - Greatly decreased money supply, which was not counteracted by the Fed so interest rates increased
- Increased interest rates and decreased optimism decreased spending, leading to significant deflation and decreases in production
    - Unemployment went up to 25%, and real output was down 30%
- Revenue act of 1932: increased taxes in order to become more fiscally responsible, but this further contracted GDP

### c. Roosevelt and New Deal

- Roosevelt immediately implemented the following reforms after taking office:
    - Declares a banking holiday where only sound banks would be able to reopen
    - Takes the US off the gold standard in 1933, allowing the USD to devalue substantially
    - Expands government spending
    - Introduces an explicit policy of increasing prices back to pre-depression levels
- "The New Deal": wide range of actions including government spending, financial rehabilitation, industrial and farm policies, social safety net, labor legislation
    - Government spending: massive public works, infrastructure projects provided jobs
        - Civil works administration: provided construction jobs in the winter of 1934
        - Civilian conservation corps: hired unemployed unmarried men to conserve and develop rural lands
        - Works Progress Administration: provided jobs on a wide array of public construction projects
    - Financial rehabilitation:
        - Recapitalized banks
        - Provided deposit insurance through newly formed FDIC
        - Bought and modified distressed mortgages through Home Owners' Loan Corporation
    - Social safety net
        - Social security act: established pensions and unemployment insurance
        - Wagner act: enabled unions with collective bargaining
        - Fair labor standards act
    - Led to massive budget deficits from 1931 onwards (up to 25% of GDP)
- Monetary policies
    - US went off gold standard, devaluing the US dollar and greatly increasing money supply $\rightarrow$ decreased interest rates $\rightarrow$ increased inflation
    - Expected inflation rose, so that real interest rates fell beginning in 1933, causing fixed investment and consumer expenditure to rise rapidly
    - Huge gold inflows starting in 1934
    - Devaluation raised the price of imported goods, especially agricultural products, and thus boosting domestic farm income
- Other inflationary policies
    - National Industry Recovery Act: Limited business competition and established minimum wages
    - Agricultural Adjustment Act: Paid farmers to limit production in order to drive up prices
- 1937 recession
    - Caused by prematurely tightening fiscal spending, causing MS to decrease significantly
    - Roosevelt had started to sound less committed to reflation, which would have lowered expected inflation and raised real interest rates

### d. Logic and role of the gold standard in Great Depression

- 1880-1914: All major countries on the classical gold standard
- Basic mechanism:
    - Each country defines its currency in terms of a certain amount of gold, promising to exchange actual gold for paper currency at this rate
    - Effectively a system of fixed exchange rates
    - MS: Money created when gold is exchanged for paper money, hence significantly limited
    - Monetary Base: Upper bounded by amount of gold in central bank
- Hume's Price-Specie Flow Mechanism: gold can help equilibrate prices and output across countries
    - If prices fall in one country, gold flows to that country due to cheaper exports, leading to higher output and inflation. 
    - As prices rise, exports become less compeititve and gold inflows decrease.
    - Trade balances, exchange rates relatively stable due to this self-correcting mechanism
- In practice, countries tampered with ratio of gold:money for purpose of stabilizing the economy
- Classical gold standard experienced few speculative runs. There was strong confidence in the system, and big countries worked together to prevent this by lending each other gold
- WWI forced many countries off the gold standard due to a need to finance the war; but when countries went back to the gold standard after, the system was much less stable
- Gold standard as a transmission mechanism for the Great Depression: when the US raised interest rates, other countries had to raise their interest rates as well to prevent gold outflows
    - Fed raises interest rates to curb inflation --> Loss of gold forces other countries to raise interest rates --> Deflation occurs for other countries which may be not in an economic boom, reducing consumer expenditure
- US was the only major country to remain on the gold standard
    - Britain had went off the gold standard due to successful speculative attacks in 1931
    - US was next in line for a speculative attack due to fears it would go off gold, possibly leading to devaluation of USD
    - To fend off this attack and prevent gold outflows, the Fed raises the discount rate = contractionary monetary policy
- Monetary policy fundamentally changed with the Fed's founding in 1914
- Eichengreen: Fed's adherence to gold standard curtailed its ability to expand MS and stimulate the economy
    - It would also call into question the US' commitment to the gold standard because lower r $\rightarrow$ gold outflows
- Friedman and Schwartz disagree:
    - US already had huge gold reserves, so outflows shouldn't be much of a concern
    - Little evidence people lost confidence in USD even after Fed raised interest rates
    - Perhaps people had irrational fears?
- Countries that exited gold standard earlier experienced less severe Depression and recovered earlier
    - Confounding factor: Leaving the gold standard was typically an act that countries were forced into by hard economic times
        - Also, speculators tend to prey on weak countries
    - However, it seems likely that all else equal countries that didnt leave the gold standard were probably doing worse than countries that did leave

### e. Friedman and Schwartz interpretation of Great Depression and event-study methodology

- Friedman and Schwartz (FS) argue that Fed did not actively raise the money supply to offset banking crises and the resulting massive reduction in MS, resulting in deflation and lower output
    - Believed that conflict existed between different Fed branches
    - Although nominal interest rates are supposed to rise due to a decreasd MS, nominal interest rates fell because inflation fell even more (MD fell even more).
- Fed actively raised interest rates from 1928 through 1932 to dissuade lending, speculative uses of credit, and loss of gold reserves
    - This further discouraged spending and reduced money supply
- Even though the monetary base did not fall, decreased use of banks (from bank failures, mistrust of banks' security) shrunk M1 and M2 due to fractional resource banking, decreasing the money supply
    - Fed failed to identify and ameliorate problems within the banking sector
- FS attempted to prove this through event-studies: comparing economy before and after a large changed in monetary policy, effectively controlling for other factors:
    - #1 January–June 1920: Raising rates to combat post-WWI inflation
    - #2 Sept/Oct 1931: Raising rates to combat speculative attack after UK goes off gold
    - #3 1932: Short-lived loosening, followed by return to tight policy
    - #4 1929–33: Lack of responsiveness to banking crises

### f. Banking crises, Diamond and Dybvig model, the “Lender of Last Resort”

- Panic of 1907: Run on Knickerbocker Trust caused a crisis of confidence fueling major bank runs and revealed the need for a lender of last resort
- Before the Fed: no lender of last resort, unit banking laws
    - Banks could only operate in one location - thus they were small, undiversified, and prone to local shocks and uncertainty
- Bank runs happen because banks only keep a fraction of total reserves
- Bank profitability depends on "maturity mismatch" - they borrow short term and lend long term
    - They play a confidence game with their depositors
    - If depositors lose confidence, banks are illiquid and will suffer large losses
    - Long-term assets are "illiquid" and cannot be provided to customers
    - Confidence = key to operation
    - Fears can become self-fulfilling prophecies
- Game Theory segue:
    - Nash equilibrium: Each player chooses the strategy that yields him/her the highest payoff given the strategies chosen by other players
    - Under the Prisoner's dilemma, both confessing is a dominant strategy
- Diamond-Dybvig model:
    - Bank takes deposits of $1 from many borrowers and lends out to project that yields a gross return of R in 2 years
    - Scenarios: you withdraw/don't withdraw; everyone else withdraws/doesn't withdraw
    - Bank can call in loan before project is finished with return r. But only at a substantial loss (gross return 0<r<1)
    - Multiple Nash equilibria: If everyone else withdraws, you withdraw. If everyone else doesn't withdraw, you don't withdraw
    - **Fear of run can become self-fulfilling. If you believe everyone else will run, your best response is to run**
        - **It is only because you think others are going to run that you decide to run**
        - If you believed no one else was going to run, you wouldn’t run
- Central bank as a "lender of last resort"
    - If a central bank had unlimited resources, it can stop banking panics through the **expectation** that it will lend to the bank undergoing a panic so that everyone can retrieve their deopsits. Thus, there is no need to run on the bank in the first place.
    - This augments the payoff matrix: if everyone else withdraws but you don't, you still receive R; if everyone else withdraws and you withdraw, you receive R
- Lender of last resort and Great Depression
    - Discount rate (rate at which Fed lends to banks) had a very limited window, making banks more susceptible to runs
    - Fed failed miserably: 9,000 banks failed
    - Deposit insurance introduced as part of New Deal, reducing reliance on Fed as Lender of last resort

## V. Great Recession
### a. Bank balance sheets, leverage, Lehman, and Financial Collapse

- Leverage is fundamental to bank operations. They borrow from depositors to make investments, applying leveraged positions to make returns
    - Leverage ratio = $\frac{\text{Liabilities}}{\text{Assets}}$
    - If value of liabilities fall 2% and leverage ratio is 20:1, then net worth falls 40%
- Lehman Brothers was the 4th largest investment bank, and operating at a leverage ratio of 30:1 (3.5% decrease in assets leads to bankruptcy)
    - Lehman had increased its holdings in real estate from 52 billion to 111 billion from 2006 to 2007
- TED spread: Difference between yield on interbank lending (LIBOR) and safe treasuries (“risk-free” rate)
    - Measure of financial risk $\Rightarrow$ Spike in this spread (large positive value) indicates that banks may be encountering insolvency problems and are restricting interbank lending, resulting in higher default risk 
- Economy had been performing well pre Recession: low unemployment rate, rising stock market, rising housing prices, and very low TED spreads
- Bear Sterns, the 5th largest investment bank, had been acquired by JP Morgan with a 30 billion loan from the Fed in March 2008
- Fannie Mae/Freddie Mac, institutions that bought mortgages in the 2nd hand market and securitized them as MBS's, they owned half of all mortgages 
    - Could borrow at low risks from banks due to implicit guarantee that government would bail them out should they fail, as they were created by the government
    - Ran at 75:1 leverage ratios
    - Put under Federal conservatorship in September 2008
- Potential solutions to Lehman
    - Buying Lehman: Lehman's toxic assets were estimated to be only worth 50% of face value
        - Barclay's had agreed to facilitate a merger, but was blocked by the Chancellor of the Exchequer
    - Government solutions
        - Nationalization
        - Bail-out: Fed provides loans to keep Lehman solvent, but Lehman was found to be higher risk than Bear, and bailing out would pose bad optics for Fed, which had just bailed out Bear Sterns (Treasury Secretary Hank Paulson known as "Mr. Bailout")
    - Bankruptcy: Ultimately, Lehman filed for bankruptcy in 2008
        - "Moral hazard fundamentalists" argued that not bailing out Lehman would send a signal to other banks
- Potential modern day bank run: if Lehman failed, then investors would want to withdraw their investments from highly levered banks, potentially toppling more investment banks
- Changes after Lehman
    - Dodd Frank act: implemented financial regulations and created financial stability oversight council in response to the recession
    - Volcker rule: restricted commerical banks from making speculative investments
    - Merill acquired by Bank of America, while Morgan Stanley & Goldman Sachs became bank witholding companies, subject to stricter regulation
    - Troubled relief access program (TARP): federal government program to buy toxic assets in order to strengthen the economy

### b. Theories of the Great Recession- Mian/Sufi and Gertler/Gilchrist

- Mian & Sufi:
    - Mortgage securitization and other sources of increased credit led to increases in household debt and housing prices 
    - Increases in housing prices led existing (as well as new) homeowners to borrow and consume more, due not only to a wealth effect but also to the alleviation of credit-constraints
    - No evidence that people invested more or paid down credit card balances. Hence, increase in debt was probably associated with increased consumption
    - Subsequent collapse in housing prices led to huge decline in aggregate demand & fall in employment
    - According to Mian and Sufi, the root cause of all of this was over-borrowing by households. The places with the largest declines in house prices were also the places with the highest pre-crisis household debt
    - Possible solution: restructuring for underwater mortgages
- Goal: validate that higher housing prices leads to more borrowing
    - Housing wealth effects: % change in consumption due to % change in housing prices
    - Due to pure wealth effects and increases in liquidity constraints from house being higher valued
- Mian/Sufi's experiment: natural experiment of land unavailability as an instrument for housing prices
    - Land unavailability: proportion of land not available for development within a certain radius
        - Areas with high land unavailability are associated with higher price increases during the housing boom, since less housing supply is available
        - This measure is exogenous from all other factors, and relevant to changes in housing prices
    - Cannot directly regress change in debt on change in housing prices due to confounding factors
    - Finds that in areas where land unavailability is high, housing prices grew significantly in the boom, causing an increase in consumption
        - Oppositely, during the recession, housing prices also fell more, decreasing spending 
        - Establishes link between housing prices and spending, due to housing wealth effects
- Gertler/Gilchrist:
    - Fall in value of bank assets and runs on banks’ short-term funding led to massive decline in bank lending
        - This fall was partly because banks held MBS as assets, which fell in value with housing prices
    - Reduced supply of bank loans decreased investment, employment etc (e.g., commercial paper market)
        - Firms (particularly small and credit-constrained ones) had to reduce employment because they were unable to borrow
    - Possible solution: liquidity injections into flailing banks to entice greater lending
- Gertler/Gilchrist's methodology: event-study on Lehman bankruptcy
    - Did the worsening of the banks’ balance sheets really cause the recession? Or was the recession caused by the worsening of the household balance sheet as suggested by Mian and Sufi?
    - Found that risk spreads peaked at the time of Lehman's collapse, an exogenous shock, which severely decreases the number of short term laons
        - Followed by decreases in durable spending and real GDP growth that lasted until spring 2009

### c. Housing boom and bust

- Housing prices rose rapidly from 2000 - 2005, leading to riskier mortgages being offered
- Housing prices began to fall due to foreclosures, quickly bursting the bubble to wipe out 50% of the gains it made over the first half of the decade
- Mortgage delinquency rates sky-rocketed from 2007

### d. Mortgage backed securities and financial innovation

- Housing mortgages were bundled together to construct tranches ordered by risk, overall reducing risk
    - These were securitized and sold as mortgage-backed-securities (MBS)
    - Investment banks sold AAA-rated MBS' to pension funds and the money market
- MBS issuance rose rapidly from 2001-2006, mirroring the house price bubble
- Off-balance sheet investment vehicles
    - Structured investment vehicles raised funds by selling short term debt to money market funds
    - Assets were a pool of mortgages or other loans
    - If assets defaulted, owners of asset-backed commercial paper can seize and sell the underlying collateral assets back to banks
        - Banks provided “liquidity backstop” to SIV’s to ensure AAA-rating
        - Effectively presented SIVs as non-risky, bank-backed investment vehicles
- Investment banks like Lehman were heavily invested in MBS, which quickly eroded in quality and value as mortgage delinquencies increased
- Repo contracts: a firm borrows funds by selling an asset at a significantly lower price (posting it as collateral) and promises to buy it back later
    - Banks like Lehman used repo contracts for short-term funding to ensure liquidity
    - Banks used MBS as the collateral asset, which rapidly lost value in this time, drying up liquidity
- Combined: decreased repo contracts from declines in asset prices led to less access to funding, and off-balance sheet SIVs required banks to pay back investors from low-quality assets
    - These factors dried up Lehman's liquidity and solvency, leading to a modern bank run
- These financial innovations were not protected by deposit insurance

### e. Housing wealth effects

- Permanent Income Hypothesis: As houses make up a significant amount of an individual's wealth, when housing prices increase, a rational person would increase their consumption over their lifetime
- Higher housing prices will make people feel richer, and then they will purchase more goods than before.
- Increase in home value could lead to more borrowing as collateral has increased, and thus more spending

### g. Bank bailouts, commitment problems, moral hazard

- Insolvent: Assets < Liabilities $\implies$ creditors are fleeing for good reason, Central Bank would make losses if it lent money
- Illiquid: Bank is solvent, but creditors are making a run such that liquidation of its assets (long-term investments) would destroy its value
- Bagehot's rule: In a crisis, lend freely, but against good collateral to institutions that are illiquid but not insolvent
    - Banks that are facing liquidity problems will have good collateral
- Problems:
    - It can be very difficult to determine true worth of collateral in the midst of a crisis
    - Many bank assets like loans don't trade on the market. Thus, it's hard to value them
    - Market value of traded assets during a crisis may not be reflective of fundamental value
- Commitment problems: based on extension of Nash equilibrium known as subgame perfect equilibrium
    - Equilibria: 
        - Bank does safe investment, government does not bail out
        - Bank does risky investment, government does not bail out
        - Bank does risky investment, government does bail out
    - In time period 1, government commits to not bailing out the bank
    - The commitment problem is if it will stick to this commitment, since if the bank chooses to do the risky investment and it fails, the government is better off bailing out the bank
- Moral hazard: knowledge that the Fed will bail out banks incentivizes risky behavior

## VI. Monetary Policy
### a. Central bank objectives

- Fed's dual mandate: low and stable inflation, full employment and GDP close to potential
- Sets monetary policy, undertakes forward guidance
- Normally independent of rest of government so that it won't be affected by political pressure
    - Politicians are myopic and want to be reelected from economic upturns
    - Trade-off between short term boom and long term inflation expectations (see expectations-augmented Phillips curve)
- Key: Central bank has unilateral power over monetary policy (interest rates) to achieve its objectives
    - Central bank may face short-run political pressure from politicians with short-run focus to lower interest rates to stimulate growth (leading to high inflation)
    - Central bank independence: isolates poltiical pressure 
- Solution: monetary policy frameworks to delineate Fed objectives clearly to everyone
    - Rules increase transparency and accountability

### b. Costs of inflation, unemployment

- Costs of inflation
    - Inflation uncertainty makes planning difficult
    - Erodes nominal wealth, wages
    - Redistributes wealth between savers and borrowers, due to fixed nominal interest rates
    - Tax brackets not indexed to inflation
    - Menu costs and sticky prices (having to continuously adjust prices), leading to inefficient resource allocations
- Costs of unemployment
    - Loss of output to society, economy
    - Loss of wages, curtailed consumption
    - Personal, pscyhological poblems

### c. Interest Rate Rules

- Inflation targeting: Central bank targets a pre-announced level of inflation (say 2%) in the medium-run 
    - Central bankers could be penalized for failing to hit the target
    - Intuitively: Central bankers use all their tools to try to hit their inflation target (like CEO’s might try to hit an earnings target)
    - However does not consider output, only inflation
    - Offers a lack of flexibility in the medium-run
    - Must also consider inflation expectations when near the ZLB. A higher inflation target would increase inflation expectations, allowing a higher real rate at the ZLB
- Taylor rule: $i_t = r_{\text{eq}} + \pi_t + \alpha \left( \pi_t - \pi_{\text{target}} \right )  + \beta \left ( \frac{Y_t - Y^P}{Y^P} \right )$
    - Typically $\alpha = \beta = 0.5$
    - $\Delta i_{t} = 1\% + 1.5 \Delta \pi_{t} + 0.5 \Delta(\frac{Y_t - Y^P}{Y^P})$
        - $\Delta i > \Delta \pi$ because we want $\Delta r > 0$ when inflation is increasing 
    - Allows CB to pursue its dual mandate as the interest rate will be a function of inflation and output gaps
    - Simple and transparent, allows agents to anticipate future rate changes
        - Less susceptible to corruption
    - Limited flexibility during a crisis (i.e. would not have been applicable in light of Fed's QE during the recession)
    - Great divergence: Fed lowered interest rates more than what the Taylor predicts during the dot-come buble bust, and interest rates have not been following the Taylor exactly since
        - Would have violated ZLB during great recession
        - One explanation: equilibrium real interest rate is no longer 2%
- Pros: simple & transparent, not susceptible to short term effects
- Cons: limited flexibility

### d. IS, Phillips, AD/AS curves

- IS curve: Decreasing relationship between the real interest rate r and output Y. It shows the combinations of r and Y such that the production of goods equals demand for goods
    - $Y = C(r) + I(r) + G + NX$
    - $\downarrow r \implies \uparrow C, \uparrow I \implies \uparrow Y$
    - Shifters (changes in Y not due to r): government spending, taxes, expected future income, Wealth, autonomous shocks to I or C 
    - **Real interest rates affect output, not nominal interest rates. However, the Central Bank can only change nominal interest rates, which basically change real rates in the short run**
- Fisher equation: $r_t = i_t - \pi_t^e$
- MP curve: describes positive relationship between inflation (x-axis) and real interest rate (y-axis), which is illustrated by the Taylor rule
- Phillips Curve: denotes negative relationship between inflation and unemployment
    - $\pi = - h(u - u^{*})$ where u* is the natural rate of unemployment (NRU)
        - NRU: Unemployment rate that would arise with “perfect market functioning”, where there is frictional unemployment - people transitioning between jobs, new-grads, etc.
        - NRU = NAIRU (Non-accelerating inflation rate of unemployment)
    - Price and wage stickiness determines how the steep the relationship is?
        - $\uparrow$ stickiness = $\downarrow$ h = Flatter Phillips curve
    - We have been observing the Phillips getting flatter recently
        - Perhaps due to Fed anchoring inflation expectations recently to low levels
        - Perhaps due to shift towards services, which has low price flexibility
- Okun's Law: $\frac{Y - Y^P}{Y^P} = - \alpha (u-u^*)$
    - As unemployment increases, output decreases
    - For every 1% increase in the unemployment rate, a country's GDP will be roughly an additional 2% lower than its potential GDP
- Aggregate Supply curve: positive relationship between inflation and output, as derived from the Phillips Curve and Okun's Law
    - Long run AS: perfectly flexible prices (AS is a vertical line)
    - Short run AS: perfectly inflexible prices (AS is a horizontal line)
- Aggregate Demand curve = IS curve + Taylor Principle
    - Central bank raises real interest rates with inflation, decreasing output/expenditures
    - Example: If inflation rises, the central bank raises real interest rates by the Taylor rule. This is a leftward movement along the IS curve, resulting in lower output
    - Thus, AD is a negative relationship between inflation and output

### e. Monetary policy implementation (corridor, floor system)

- Open market operations:
    - It would increase the FFR by selling Treasury bills on the open market in exchange for money
    - This reduces the amount of money in circulation ($\downarrow$ MS) and increasing the nominal interest rate
- Corridor system:
    - Central bank chooses a narrow corridor around the target nominal interest rate i: $[i_L, i_H]$
    - It will supply an arbitrary amount of reserves at $i_H$, the discount rate, and to take arbitrary deposits at $i_L$, the deposit rate
    - Effectively, it will only pay out interest at $i_L$ and receive interest at $i_H$. Funds traded  for any $i \in [i_L, i_H]$ is done on the private market, between banks
    - Central bank shifts supply of reserves through Open Market Operators, achieving interest rates in the corridor
    - Industry standard: ECB, Bank of England, etc.
    - Open market operations serve to position interest rates within the corridor
- Floor system:
    - Keep nominal interest rate at or near the lower bound of the corridor: $i_L$
    - Requires enough reserves (supply) to "push" interest rate to the floor of the corridor, which the Fed has achieved due to QE
    - Interest on reserves = Risk-free market interest rate, so as to ensure financial institutions would deposit reserves with the Fed
    - Key change: Fed starts to pay interest on reserves in 2008
    - With the Fed paying interest on excess reserves and its balance sheet being large, the Fed is actually operating on a floor system where the interest on excess reserves is the target policy rate
    - Floor systems allow Central Banks to separate interest rate targets from liquidity concerns (open market operations). Without the interest rate floor established by the corridor, such an injection of reserves could push the policy rate well below its target.

### f. ZLB & Unconventional monetary policy (forward guidance and quantitative easing)

- Zero Lower Bound: The Fed's ability to set monetary policy becomes ineffective when interest rates approach 0%
    - Traditional argument: money pays 0 interest, so any lower and people would just hold cash
    - Some European countries have dabbled with negative short-term interest rates up to 0.8% in 2017: Germany, Sweden, Switzerland
    - It turns out, in the short-run, “lower bound” on interest rates is slightly below zero ("effective lower bound" < ZLB) because cash-storage capacities are limited
    - In the long-run, companies specializing in holding money may emerge
- Traditional Open-Market Operations only bought short term Treasury bonds, bought when FFR is near 0 in a recession, this does not mean that firms are willing to lend at 0% due to risk
    - Traditional Open-Market Operations change very short term rates (literally the overnight lending rate)
- Bond yield formula: $i_t^{10y} = \frac{1}{10}(i_t^{1y} + \mathbb{E}[i_{t+1}^{1y}] + \cdots + \mathbb{E}[i_{t+9}^{1y}]) + \text{risk premia}$
    - Open-Market Operations affects shortest-term rate: $i_t^{1y}$
- Forward guidance: Central Bank promises to keep Fed Funds rate low in the future
    - Goal: Lower long-term real rates (even though short term nominal rate is at zero) reduces the spread between short and long term bonds
        - Encourages firms to increase spending
    - The central bank’s clear messages to the public are one tool for preventing surprises that might disrupt the markets and cause significant fluctuations in asset prices
    - Lower expected future short rates $\Rightarrow$ lower current long rates (long rates are average of expected future short rates) $\Rightarrow$ lower mortgage rates $\Rightarrow$ higher spending
    - Lowers $E[i_{t+1}^{1y}], ...$ and higher $\pi^e$ $\Rightarrow$ real interest rates increase
    - Encounters the commitment problem: if we leave the recession and inflation rises, will the Fed continue to keep its promise of low interest rates?
        - Requires holding interest rates low for longer than is justified by the current economic conditions, so that it cannot be covered by the Taylor rule
    - Typical wording: "some time", "extended period", "well anchord", "considerable time", etc
- Quantitative easing: Central Bank Purchases of risky and long-term assets with the goal of lowering spread between yield on risky assets and FFR (depresses risk premia between risky and safe assets)
    - These assets can include MBS, Treasuries, risky bonds
    - Fundamentally different from open-market operations as the Fed is not purchasing risk-free Treasury bills but risky (non-traditional) assets
    - Goal: Increase the money supply and provide banks with liquidity, allowing them to increase lending, while decreasing risk (lower risk premia) and uncertainty in the market 
    - From late 2008 to 2010, the Fed rapidly increased its balance sheet through 3 successive rounds of QE
    - In 2013, the Fed announced a "tapering" of some of its policies contingent upon continued positive economic data
- Quantitative easing can also increase inflation, decreasing real interest rates at the zero lower bound 

## VII. Price rigidity and Phillips curve

### a. Classical and Keynesian Views

- Extreme classical view: prices adjust quickly, AS is vertical
    - No point to monetary/fiscal stimulus that increase AD: output doesn't respond to fiscal/monetary stimulus, instead only inflation responds to stimulus
    - Believes that output growth arises from supply shocks only
    - More accepted for the long run
- Extreme Keynesian view: sticky prices, AS is horizontal
    - Hence, output responds to fiscal/monetary stimulus, while inflation does not
    - Suggests that recessions due to AD shocks can be fixed by monetary/fiscal stimulus that increase AD
    - More accepted for the short run
- Theories of price rigidity: 
    - Fear of antagonizing customers
    - Imperfect attention: firms have other worries
    - Menu costs
    - Worry that competitors won't change prices
- Theory of wage rigidity: 
    - Moral or personal issue of cutting wages
    - Labor contracts
    - Limited managerial attention

### b. Expectations augmented Phillips curve

- Old Keynesian Phillips curve: $\pi = - h(u - u^{*})$
    - If this relationship were constant, then we could permanently reduce unemployment by just accepting a bit more inflation
    - Problem: What happens if we come to expect inflation? Firms will just start to anticipate high inflation, raising prices in advance
- Expectations augmented Phillips curve: $\pi = \pi^e - h(u - u^{*})$
    - Firms raise prices not only when the economy is overheated (u < u*), but also simply in anticipation of future inflation
    - Typically assume that last year's inflation is this year's inflation expectations: $\pi_{t - 1} = \pi_t^e$ 
    - Inflation expectations can shift the Phillips curve, creating a painless way of curbing hyperinflation
    - Leads to inflation spiraling: if inflation is growing, people constantly expect increased inflation, further worsening it

### c. 1970’s US “Great Inflation”, Volcker disinflation (RIP)

- Common interpretation: The Fed attempted to target u < u*, overheating the economy
    - Since they were employing the Old Keynesian Phillips curve, they did not factor in inflation expectations
    - Political pressures to lower unemployment in the short-run, ignoring long-run inflationary pressures
    - Exogenous oil price shocks in 1973, 1979
        - Can be interpreted as shifts in u* in the augmented Phillips curve model
- Inflation became "public enemy number one"
- Sacrifice ratio: output that must be lost (sacrified) in order to achieve a given reduction in inflation: $\frac{\Delta Y}{\Delta \pi}$
    - In the late 1970s, when inflation was at its peak, economists believed the sacrifice ratio was very high
    - Okun predicted it was 10: 10% decrease in inflation entailed a 100% decrease in output
    - Many were skeptical bringing down inflation was worth the significant cost to output
- Volcker becomes Fed chairman in October 1979. He immediately set a target inflation rate of 4% and dramatically raised interest rates, which also raised unemployment
    - Falling inflation also dramatically reduced inflation expectations
    - Evidence for expectations augmented Phillips curve: sacrifice ratio during Volcker disinflation was 1.8, much lower than predicted in 1979
- In the short-run, there was a severe recession where unemployment increased to 9.5%, but inflation decreased to 3.3%
- Short-term pain for long-term gain: inflation has hovered around 2% since the late 1990s
    - Argument that Volcker set the precendent for the Fed making good on its threat of combatting inflation at all costs through massively high interest rates

### d. Hyperinflation (500%+ per year)
- Sargent: "hyperinflations are always and everywhere a fiscal phenomenon"
    - Caused by governments printing money from spending beyond their means
- Seignorage: implicit tax from the reduction in purchasing power from government expanding money supply
- Shock therapy: sudden reduction of government spending through decreased subsidies, economic liberalization, privatization in order to balance the budget
    - Used in Bolivia by Jeff Sachs, also in Argentina
- To bring down inflation at low cost of unemployment, central bank must commit to a low level of inflation and act decisively to convince the public
    - Once the public is convinced, the expectations augmented Phillips curve model will decrease inflation naturally through lower inflation expectations
    - However, very challenging to do since central bank may be challenged to reduce interest rates for economic upturns
        - Politicians are myopic!


## VIII. Fiscal stimulus and consumption responses

### a. Fiscal multiplier, Marginal Propensity to Consume

- Friedman's Permanent Income Hypothesis: consumers are forward looking and smooth their consumption throughout their lifetime (based on their permanent income)
    - Implies that marginal propensity to consume is near 0, since an increase in income will be spread throughout the individual's lifetime
- Fiscal Stimulus: increases government spending or reductions in taxes
    - Had fallen out of favor in subsequent decades after Great Depression until the Recession (ARRA)
- Fiscal Multiplier: if the government spends 1$, how much does output rise by?
    - 1x multiplier: no 'rippling' effects; MPC = 0
    - 0x multiplier: government spending 'crowds out' private spending
- Classical view: 0x multiplier, crowding out occurs from fiscal stimulus
    - No effect on output since government spending replaces private spending
    - More likely to be true when economy is at full capacity
- Keynesian view: resources in economy are not efficiently allocated, so that government spending will not be crowded out, and that output can be increased

### b. Keynesian logic for fiscal stimulus and Frictions in the Economy

- Keynes argued government spending should be used in recessions to stimulate aggregate demand
    - However, to be efficient, government must be more productive than private sector
- During a recession, economy is not productive due to high unemployment, so that government spending increases productivity and takes advantage of wasted resources
    - Recessions involve high unemployment. A “social planner” would want to put those workers to work as the economy is “wasting” the manpower associated with these unemployed workers
    - Increasing government spending raises Y closer to Y*, taking advantage of wasted resources
    - Such government expenditure should be done even if the government is inefficient at producing things relative to the private sector - who else would do it?
- MPL and MRS
    - Firms hire until MPL = wage, and households work until MRS = w, so that MPL = MRS in a perfect economy
    - Can compute the MPL/MRS ratio as a measure of frictions in the economy
        - High MPL/MRS: nobody is working as they substitute away to leisure
        - Low MPL/MRS: everyone is working as there is no incentive to substitute away to leisure
    - During the last recession, frictions no longer allowed the economy to operate at optimal Y*
    - MPL/MRS spiked up (prices, wages too high, substitution cost very low), so that government can use fiscal policy to reduce frictions

### c. Aggregate vs. relative fiscal multiplier

- Aggregate fiscal multiplier: when government spending increases by 1$, how much does output overall change?
    - Confounding factor: monetary policy may cause interest rates to change (e.g. due to Taylor rule), leading to 'crowd out'
- Fiscal policy typically will raise interest rates, but being at the ZLB reduces interest rate increases, reducing crowding out to make it more effective
- States vary on their level of military spending
- Relative fiscal multiplier: when government spending increases by 1$ in California relative to Illinois, how much does output increase California relative to Illinois? (CA is a high military spending state while IL is a low military spending state)
    - e.g. when military spending increases by 1% in CA relative to IL, output increases by 1.5% in CA relative to IL
- Since interest rates are uniform across states, the relative fiscal multiplier will be larger than the aggregate fiscal multiplier, since the aggregate fiscal multiplier is subject to changes in interest rates and consequent crowd-out
- This makes the relative fiscal multiplier like the aggregate fiscal multiplier, when monetary policy is unresponsive
    - **Natural variation in military across states but homogeneity in interest rates creates a natural experiment that removes interest rates as an endogenous variable**
- Results are consistent w/ Keynesian view that fiscal multiplier can be quite large if monetary policy is unresponsive


### d. Interpretation and estimates of MPC, empirical methods (e.g., Johnson, Parker and Souleles papers)

- Government sent rebates to individuals/households totaling 100 billion in 2008 as part of the Economic Stimulus Act
    - However, timing of check was randomized (based on social security number)
- Measure of change in consumption: $C_{i,t+1} - C_{i,t} = \sum_s \beta_s \text{Month}_s + \mathbf{\beta_1 X_{i,t}} + \beta_2 R_{i,t+1} + u_{i,t+1}$ 
    - If doing indicator version of rebate: $C_{i,t+1} - C_{i,t} = \sum_s \beta_s \text{Month}_s + \mathbf{\beta_1 X_{i,t}} + \beta_2 \mathbb{1}(R_{i,t+1}) + u_{i,t+1}$ 
    - If rebate received in period t, then $R_{i,t} = 300$ for individuals and $R_{i,t+1} = 0$, so that the difference in consumption between t and t+1 due to the rebate is measured by $\beta_2$, which is the MPC!
    - 2 stage OLS approach (because not everyone received the same rebate amount)
        - 1st stage: OLS of $R_{i,t}$ on $\mathbb{1}(R_{i,t})$
        - 2nd stage: OLS of $\Delta C_{i, t+1}$ on fitted $R_{i,t}$
- Found through above approach an MPC of 0.25 for non-durable goods 
- Typically durable goods are consumed over a longer period, so that its consumption can be 'spread out' over many periods and hence is not representative of temporal consumption

### e. US debt and deficits, ARRA stimulus

- American Recovery & Reinvestment Act: 780 billion in scale, with 38% as tax reductions, 34% to state and local governments, and 28% as direct Federal aid
- Government had began achieving budget surpluses in the late 1990's, but dot-com bubble led to decreases in tax revenue, followed by war on terror and the Bush tax cuts
- Discretionary spending has been falling, but mandatory spending (e.g. social security, medicare) has significantly increased
- Current US expenditure: 23% of GDP, current US revenue: 18% of GDP
- Other countries like Japan have a ~200% debt to GDP ratio, while US is almost at 100%



## IX. Macro finance
### a. Expectation hypothesis of term structure

- Gross return: $\frac{P_{t+1}}{P_t} - 1= i_t$
- Net return: $\frac{P_{t+1} - P_t}{P_t} = i_t$
- Bonds: promises to pay some money in the future (coupons), and the face value by the time of maturity
    - Price and yield are inversely correlated: when Fed buys bonds, prices go up and MS expands, decreasing interest rates (and vice versa)
    - Yield and interest rates are correlated
- Term structure in 2 periods
    - 2 year bond's total yield: $(1+i_{2y,t})^2$ where $i_{2y,t}$ is the 2 year yield
    - 2 1-year bonds' total yield: $(1+i_{1y,t})(1+i_{1y,t+1})$
    - Hence, $i_{2y,t} \approx \frac{i_{1y,t} + i_{1y,t+1}}{2}$
- This derives the term structure formula: $i_{m, t} = \frac{i_t + i_{t+1} + ... +i_{t + m - 1}}{m}$ 
    - Long-term nominal interest rate is the average of expected future short-term interest rates

### b. Real vs. nominal interest rates, TIPS, Yield curves

- Yield curve: plots maturity to yield
    - Typically as maturity increases, yield increases due to increased risk and uncertainty (from inflation and illiquidity) in the long term
    - Inverted yield curve: when long term bonds have a lower yield than short term bonds; this means that future interest rates are lower than today's rates
        - Is correlated with a recession: people expect lower interest rates in the future
- Treasury Inflation-Protected Securities (TIPS): bonds that are indexed to inflation, so that the yield is correlated with the real interest rate
    - $i_{m,t} \approx \frac{r_t+r_{t+1}+\cdots+r_{t+m-1}}{m} + \frac{\pi_t+\pi_{t+1}+\cdots+\pi_{t+m-1}}{m}$
    - Can use difference between yields of same-maturity nominal bonds (nominal interest rate) and TIPS (real interest rate) to determine expected inflation

### c. Bond and stock pricing- connection to monetary policy and macro announcements

- FOMC announcements signal about future plans for interest rates (forward rates)
- Effects of FOMC announcements on future rates can be seen immediately in the change in price of bonds
    - Typically only has effect on short term rates
- Interest rate changes is empirically correlated with decreases in output
    - Fed's outlook signals recessions or booms, affecting people's expectations
- Bond prices: $P_t = \frac{C_t}{1+i_t} + \frac{C_{t+1}}{(1+i_t)(1+i_{t+1})} + \cdots + \frac{F_{t+N}}{(1+i_t)(1+i_{t+1})\cdots(1+i_{t+N})}$
    - Real: $P_t = \frac{RC_t}{1+r_t} + \frac{RC_{t+1}}{(1+r_t)(1+r_{t+1})} + \cdots + \frac{RF_{t+N}}{(1+r_t)(1+r_{t+1})\cdots(1+r_{t+N})}$
    - Inflation will decrease bond price (via increasing nominal interest rates) and hence increase yield $( \uparrow P = \downarrow Y )$
    - In a recession, bond prices will increase as nominal interest rate is lowered
- Stock prices: $P_t = \frac{D_t}{1+i_t+\rho_t} + \frac{D_{t+1}}{(1+i_t+\rho_t)(1+i_{t+1}+\rho_{t+1})} + \cdots$
    - Real: $P_t = \frac{RD_t}{1+r_t+\rho_t} + \frac{RD_{t+1}}{(1+r_t+\rho_t)(1+r_{t+1}+\rho_{t+1})} + \cdots$
    - Inflation has an indeterminate effect on stock price, since dividends and inflation both increase
    - In a recession, stock prices are indeterminate since inflation, dividends decrease, but risk increases


### d. Announcement effects and “event study” empirical methodology

- Responses to employment reports: high employment $\rightarrow$ increased inflation $\rightarrow$ decrease in stock prices
    - Employment reports are an indicative measure of the health of the economy
    - Inlation decreases bond prices but increases bond yield 
- As prices are the present value of future expected cashflows, we are more interested in the "surprise" announcment instead of the actual announcment
    - In the lead up to announcements, projections or approximations of the actual announcement will cause prices/yields to adjust accordingly
    - By the time the actual announcement occurs, if the announcement = projections, then prices/yields will not change at all as that information has already been fully incorporated into prices
    - If announcment != projections, then the sudden correction in prices/yields will indicate direct effects of the announcement on the market, creating opportunities for event studies


## X. Exchange rates and Open Economy
### a. Nominal vs. real exchange rate

- Nominal exchange rate: $e_{nom} = \frac{\text{units of foreign currency}}{\text{units of domestic currency}}$
    - If $e_{nom}$ increases, domestic currency appreciates as 1 unit of domestic currency can now buy more foreign currency 
    - If $e_{nom}$ decreases, domestic currency depreciates 
- Carry trade: deciding in what currency to hold money in, factoring in expected interest rates and exchange rates
    - Can hold money in domestic currency with returns $1+i$
    - Can also exchange money to foreign currency at $e_{nom}$, hold with returns $1+i_{FOR}$, then switch back
    - Both alternatives should offer the same returns, or else arbitrage occurs: $1+i = (1+i_{FOR}) \frac{e_{nom}}{\mathbb{E}[e_{nom}]}$
- Real exchange rate: $e \equiv e_{nom}\frac{P}{P_{FOR}}$
    - Price of foreign good in dollars: $P_{FOR}^{USD} = \frac{P_{FOR}}{e_{nom}}$
    - $\Rightarrow e = \frac{P}{P_{FOR}^{USD}}$ (Price ratio of domestic to foreign good)

### b. Relative PPP and relationship between inflation and exchange rates 

- Change in real exchange rate: $\%\Delta e= \%\Delta e_{nom} + \pi - \pi_{FOR}$
- Absolute PPP: implies that e = 1 (price ratio of domestic to foreign good) or else there will exist arbitrage opportunities
    - Does not hold empirically: there exists non-tradeable goods
    - Law of one price: $P_{FOR}^{USD} = P$
- Relative PPP: growth rate of real exchange rate tends to a fundamental value (0 in the long-run), i.e. price ratios between countries stays constant
    - Implies that $\%\Delta e = 0$, so that $\%\Delta e_{nom} = \pi_{FOR} - \pi$
    - This derives a relationship between inflation and changes in nominal exchange rate in the long-run

### c. Fixed vs. flexible exchange rates, “impossible trinity” 

- Fixed exchange rate: commitment by central bank to keep exchange rate fixed against a foreign currency at a certain ratio ("peg")
    - Will actively intervene in currency market, buying foreign currency by printing domestic currency or selling foreign currency through foreign reserves
    - Implies that $\%\Delta e_{nom} = 0$, so that $\pi_{FOR} = \pi$
    - Typically fixed to USD
    - Pros:
        - Displays credibility and commitment of central bank
        - Prevents hyperinflation
    - Cons:
        - Does not allow for independent monetary policy or free-flowing capital
        - If there is no independent monetary policy, then especially unoptimal if 1 country is in a boom and another is in a recession
        - If capital controls exist, then foreign investment is discouraged
- Impossible trinity: cannot have all 3 of independent monetary policy, fixed exchange rate, and no capital controls
    - Say CB has a fixed exchange rate and lowers domestic interest rates. Investors wish to shift funds abroad. CB needs to purchase domestic currency using forex reserves to maintain currency peg. It loses forex reserves converting domestic currency to foreign currency for investors leaving country. The result: either they are unable to maintain peg (lose fixed exchange rate) or they institute capital controls to protect forex reserves.
- Use of capital controls has massively declined since 1980's

### e. The EMS crisis: Exchange rate crises and speculative attacks

- European Monetary System (EMS): system of fixed exchange rates, in which each country fixed its exchange rate to other European countries
- Fall of Berlin Wall led to GDP growth & inflation in Germany (IS curve shifts right), causing Germany to begin to raise interest rates in order to bring output back to normal 
- Neighbors (UK and Italy) benefitted from increased exports (IS curve shifts right)
- UK and Italy would also have to raise interest rates to maintain the exchange rate
    - In fact, UK and Italy would have to raise interest rates even more to prevent currency attacks and capital flight, since their IS curves do not shift out as much as Germany's did
    - UK and Italy would have to sell Deutsch Marks and buy pounds to keep the exchange rate similar, as investors were seeking to move their money to Marks (higher interest rate)
    - Illustrates issue of no fiscal union or adverse shocks reverberating across borders
- Black Wednesday: Bank of England raised rates from 10 to 12 to 15% in 1 day
    - By 7 PM, the UK announced it was leaving the EMS
    - Soros had bet that the GBP would devalue and that the UK Central Bank could not maintain a fixed exchange rate, so he opted to sell pounds for marks
    - GBP does devalue significantly, Soros earns a lot on this bet (presumably converted marks back to pounds at the far lower rate)
- These tensions caused the break-up of the EMS. Several countries shifted to floating regimes, others devalued and stayed within the system
- EMS was the pre-cursor to the EU area - a monetary union of 19/28 EU countries
- When should a country peg?
    - Benefits are high when: there is large potential for trade, possibility for unified fiscal policy
    - Costs are high when: business cycles are not aligned, labor markets inflexible, fiscal union not possible

## XI. Additional topics
### a. Recent trends in unemployment vs. employment-to-population (epop) ratio

- Employment rate: ratio of employed to working age population
- Unemployment rate: ratio of unemployed to labor force (more restrictive denominator)
- % of employed prime age workers has increased from ~60% in 1950 to ~80% today
    - Mainly driven by female employment and labor force participation 
    - However, males' participation rates have decreased since the 50's, and even females' has started declining this decade.
        - % of living w/ parents has decreased, especially among the non-employed; but this can also be explained by having larger houses
    - Participation rates associated with education level: those with a college degree typically have higher participation rates than those w/ a HS degree
- Hours worked has significantly decreased since 70 hrs/wk in the 19th century to ~40 hrs/wk


### b. Recent trends in inequality, labor share

- Inequality decreased during Roosevelt but increased significantly since the 80's, and now we are back to the roaring 20's levels
    - Top 10% and especially top 1% has seen their share of pre-tax income increase over the last 30-40 years
- Explanations
    - Skill biased technical change
    - Outsourcing and automation
    - Changes in tax systems (tax reductions from Reagan, Bush)
    - Erosion of worker bargaining power (unions)
### c. Argentina's financial crises

- Basic overview
    - Post-WWII, Argentina became averse to its exports-based economy being so affected by geopolitics in Europe
    - Peron comes to power, advocating for import-substitution, significant government spending on infrastructure and welfare, strong labor unions with high wages
    - Strong inflationary pressure due to wages and government expenditure
    - Budget deficit and debt balloons, so the government prints more money, reducing the public's purchasing power
    - Hyper-inflation, multiple debt defaults, 3 new currencies between 1974-1991
- Cavallo's plan
    - Established a currency board that backed the nation's currency with USD at a fixed exchange rate of 10,000 Australs to 1 USD
    - Created a new currency, the Peso, that was convertible from the old currency at 10,000 Australs to 1 Peso, effectively establishing a 1:1 convertibility between Pesos and USD
    - This should remove the Central Bank's ability to print money and increased the new currency's credibility
    - Cavallo removed protectionist measures, shifted away from import-substitution, privatized money-losing state-run industries
    - Increased government's ability to finance its debt payments, reduced reliance on government expenditure for production, curtailed inflationary pressures
- Problems emerge: unemployment, lower tax revenues, banking crises
- End of 2001: Argentina defaults on its debt, currency board abandoned
- 2016: Issues first bonds since 2002
- Macri's economic policies
    - Lifted capital controls, settles debt disputes to re-establish credibility, decreased deficits, inflation targeting (5%), policies to increase investment
    - Accused of being too gradual, Peronists (Kirchner) return to power

### d. Japan: financial crisis, “lost decade” and Abenomics
- Saw significant post WWII growth, catching up the UK by the 1970's
- Inflation spiked in the 70's but fell to around 0% in the 90's
- Bank of Japan began to raise interest rates from 2-4% in 1989 to burst the bubble and curb inflation
    - This led to the stock market falling by 50%, leading to bailouts of highly levered companies
    - Also led to a real estate crash much larger than that of the US during the recession
        - This further worsened banks' situations due to being heavily invested in mortgages (similar to 2008 financial crisis)
- Nominal GDP growth fell from 6% in 1980 to -0.5% in 2000
    - But effect is smaller if accounting for hours worked: work week went from 45 to 38 hours a week due to changes in labor standards laws
    - Unemployment grew to 5% in 2000, which is high for Japan
    - Lost decade: 1991 - 2000, a period of economic stagnation following asset price bubble's bursting in 1991
- Female participation has not yet converged to male participation as much as that seen in the US 
- Significant aging population
- Abenomics
    - 1st arrow: monetary policy
        - Had already hit ZLB in 2000s
        - Relied on unconventional monetary policy, especially quantitative easing, buying short and long term bonds and ETFs to increase inflation expectations and decrease real rates
        - QE can also increase inflation, decreasing real interest rates at the zero lower bound
        - Led to depreciation of JPY (increased exports)
    - 2nd arrow: fiscal policy
        - 10 trillion JPY stimulus package
        - Debt to GDP ratio at 250%
        - Despite significant borrowing and a high debt to GDP ratio, bond yields stayed low, indicating no worry of defaulting
        - The probability of a country to default on its debt depends on its capacity for structured reform
    - 3rd arrow: structured reform
        - Replenish work force’s aging population, increase women participation in work force, invest in “health and longevity” industry
            

# Assignment Solutions

https://hackmd.io/@7eWLFRl9T9SBRxXxhjpyzg/rkhoJnlRS/edit

# Reading Notes

https://hackmd.io/@umaniku/S15Z-nxCH

