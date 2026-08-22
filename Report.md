# M26 Data Analytics I - Assignment 1 Report


## 1. Data Cleaning Methods
This section outlines the preprocessing steps applied to both datasets to ensure readiness for modelling and visualization.

### 1.1 Bank Term-Deposit Data (bank.csv)
(Partner fills in: Describe how missing values were handled, how the balance was cleaned, and any specific vectorized string or date manipulations used before grouping.)

### 1.2 NYC Airbnb Listings Data (listings.csv)
Vectorized Price Conversion: The price column originally contained string objects formatted with currency symbols and commas (e.g., "$113.97"). Using pandas' vectorized .replace() function with regular expressions (r'[\$,]'), these characters were stripped, and the column was cast to a float for numerical analysis. Rows with missing prices were dropped.

Vectorized String Parsing for Amenities: The amenities column was stored as a JSON-like string of lists. We utilized pandas' vectorized .str.contains() method (with case=False) to efficiently create boolean feature flags for key amenities (Gym, Pool, Elevator, Hot tub, Pets allowed) without requiring slow, row-by-row iteration. We also used ast.literal_eval to safely parse the string and calculate a total amenity_count.

Date Transformations for Maturity Indexing: The first_review and last_scraped string columns were converted to pandas datetime objects using pd.to_datetime(). This allowed for vectorized date math to calculate maturity_years (years since the first review).

## 2. Summary of Findings

### 2.2 Part II: Airbnb Market Insights

#### Price Segmentation & Market Overview (Q1)
The market was segmented into three equal tiers. The Budget tier is heavily dominated by Private Rooms in Brooklyn, while the Luxury tier predominantly consists of Entire Homes/Apartments in Manhattan.

#### City-Level Comparative Analysis (Q2)
Manhattan commands a significant price premium across all property types. Notably, Manhattan heavily dominates the commercial "Hotel room" segment (averaging $818/night compared to Brooklyn's $385/night). Conversely, Brooklyn's residential segments (Entire home/apt) offer larger average guest capacities despite lower average prices.

#### Location-Based Premium Analysis (Q3)
Listings in "Prime" neighborhoods (defined as the top 25% of median prices within a borough) charge a substantially higher price-per-guest. Interestingly, this premium is not justified by a vastly superior number of amenities (which remain relatively flat), but rather slightly higher guest capacities and the intrinsic value of the location itself.

#### Value-for-Money Opportunities (Q4)
The outer boroughs offer the best value (measured by guest capacity per dollar). The Bronx and Staten Island consistently provide the most space for the lowest cost. The absolute best value segments are Entire Homes/Apt in Staten Island and the Bronx, and Shared Rooms across all boroughs.

#### Feature & Amenity Impact on Price (Q5)
The presence of a "Gym" provides the highest overall price premium in NYC, particularly in Manhattan. Notably, the "Superhost" designation actually correlates with slightly lower prices across most boroughs, suggesting these hosts prioritize high occupancy and competitive pricing over luxury markups.

#### Timeline & Readiness Effect on Pricing (Q6)
Listings with "Limited Availability" (1-15 days open in the next 30) generally command higher prices than those that are fully booked or readily available, indicating a scarcity premium. Additionally, newer listings (<1 year) in Manhattan charge more than "Veteran" listings, suggesting that novelty or newer furnishings command a higher price than an established review history.

#### Host Impact on Listings (Q7)
Portfolio size directly impacts pricing. "Large Portfolio" hosts (21+ listings, acting as corporate developers) charge the highest average prices ($317) compared to "Single Listing" hosts ($262). While these corporate hosts charge more, they offer highly standardized amenities rather than the personalized touches of a casual host.

