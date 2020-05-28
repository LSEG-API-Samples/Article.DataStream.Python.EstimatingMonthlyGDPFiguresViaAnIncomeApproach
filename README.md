# Estimating Monthly G.D.P. Figures Via an Income Approach
Only quarterly U.S.A. G.D.P. data is published; this article describes a method of estimating monthly such figures using monthly Total Compensation figures.

## Introduction

Gross Domestic Product (G.D.P.) is often thought of and calculated with an Expenditure Approach such that $GDP = C + I + G + (X - M)$ where $C$ = Consumption, $I$ = Investment, $G$ = Government Spending, & $(X – M)$ = Net Exports, but it is also possible to calculate it via a per worker Income Approach. With this approach, we may estimate G.D.P. Per Worker (G.D.P.P.W.) with Total Compensation Per Worker (T.C.P.W.) figures such that (as per Appendix 1):

$$\text{(Real GDP Per Worker)}_t  = \frac{r_{t}}{r_{t-1}} \frac{\text{(Real National Total Compensation Per Worker)}_{t}}{\text{(Real National Total Compensation Per Worker)}_{t-1}} \text{   (Real GDP Per Worker)}_{t-1}$$

where $r_t = \frac{\text{(Real GDP Per Worker)}_t}{\text{(Real National Total Compensation Per Worker)}_{t}}$.

We can then attempt to interpolate G.D.P.P.W. values at higher frequencies than they are officially released with higher wage/income figure releases (*exempli gratia* (e.g.): to **compute monthly G.D.P. figures when only quarterly ones are released using monthly published Total Compensation data**).

We have to be careful of a few difficulties outlined by [Feldstein (2008)]( https://www.nber.org/papers/w13953) (MF hereon): "*The relation between productivity* [ *id est* (i.e.): G.D.P.] *and wages has been a source of substantial controversy, not only because of its inherent importance but also because of the conceptual measurement issues that arise in making the comparison.*" (Feldstein (2008)). MF outlines several key factors (KF hereon) to consider when studying the question:

1.	"[An undeserved] *focus on wages rather than total compensation.  Because of the rise in fringe benefits and other noncash payments, wages have not risen as rapidly as total compensation.  It is important therefore to compare the productivity rise with the increase of total compensation rather than with the increase of the narrower measure of just wages and salaries.”* This is why this article will first focus on using [Total Compensation (TC)](http://product.datastream.com/browse/search.aspx?dsid=ZRQW955&AppGroup=DSAddin&q=USPERINCB&prev=99_aUSDGPY%2FA&nav_category=12&nav_market=United+States).
2.	“[… The] *nominal compensation deflated by the CPI is not appropriate for evaluating the relation between productivity and compensation* […] *this implies that the real marginal product of labor should be compared to the wage deflated by the product price and not by some consumer price index.* [...] *The CPI differs from the nonfarm product price in several ways. The inclusion in the CPI, but not in the nonfarm output price index, of the prices of imports and of the services provided by owner occupied homes is particularly important.*" This is why this article will first focus on using Nominal T.C. deflated (made 'real') with the [Nonfarm Business Sector Output Price Index Deflator (NBSOPID)](http://product.datastream.com/browse/search.aspx?dsid=ZRQW955&AppGroup=DSAddin&q=Nonfarm+Business+Sector+real+2012%3D100&prev=99_Nonfarm+Business+Sector+real+2012%3D100&nav_category=12&nav_source=Bureau+of+Labor+Statistics%2C+U.S.+Department+of+Labor).

Keeping these points in mind, we will attempt to investigate the relationship between the [United States of America( U.S.A.)'s Real G.D.P. (R.G.D.P.)](http://product.datastream.com/browse/search.aspx?dsid=ZRQW955&AppGroup=DSAddin&q=USGDP...B&prev=99_USCP...CE&nav_category=12&nav_market=United+States) and U.S.A.'s Real National Total Compensation (R.N.T.C.) in order to construct a framework allowing us to estimate **monthly** R.G.D.P. data when only quarterly data is published.

## Numerical Approximation

### Background

As per Appendix 1:

$$\begin{array}{ll}
    \frac{RGDPPW_t}{RGDPPW_{t-1}}
        &=  \frac{r_t}{r_{t-1}} * \frac{RNTCPW_{t}}{RNTCPW_{t-1}}
        & \text{where } r_t = \frac{RGDPPW_t}{RNTCPW_{t}} \text{. Therefore} \\
     \widehat{RGDPPW_t} &
        = \frac{\widehat{r_{t}}}{r_{t-1}} * \frac{RNTCPW_{t}}{RNTCPW_{t-1}} * RGDPPW_{t-1}
        & \\
\end{array}$$

It may seem needlessly convoluted to insert $r_t$ the way it was done above, but it was necessary due to the fact that we have $r_t$ estimates ($\widehat{r_{t}}$) - we thus build our framework around it: since Total Compensation figures are released on a monthly basis, if we can construct an estimate for the linearly-time-variant $r_t$, we can then construct monthly G.D.P. figures (even though only quarterly ones are published). \
This article will study the efficiency of the U.S.A. Real G.D.P. Per Worker To National Real Total Compensation Per Worker Ratio ($RGDPPWTNRTCPWR$) as the ratio '$r_t$'.

## Development Tools & Resources
The example code demonstrating the use case is based on the following development tools and resources:

- Refinitiv's [DataStream](https://www.refinitiv.com/en/products/datastream-macroeconomic-analysis) Web Services (DSWS): Access to DataStream data. A DataStream or Refinitiv Workspace IDentification (ID) will be needed to run the code bellow.
- Python Environment:
Tested with Python 3.7
- Packages: DatastreamDSWS, [Numpy](https://numpy.org/), [Pandas](https://pandas.pydata.org/), [statsmodel](https://www.statsmodels.org/stable/index.html), [scipy](https://www.scipy.org/) and [Matplotlib](https://matplotlib.org/). The Python built in modules [statistics](https://docs.python.org/3/library/statistics.html), [datetime](https://docs.python.org/3/library/datetime.html) and [dateutil](https://dateutil.readthedocs.io/en/stable/) are also required.
