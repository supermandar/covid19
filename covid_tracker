import matplotlib.pyplot as plt
from matplotlib.dates import DateFormatter
import matplotlib.ticker as ticker


# Section 2 - Loading and Selecting Data
df = pd.read_csv('https://raw.githubusercontent.com/datasets/covid-19/master/data/countries-aggregated.csv', parse_dates=['Date'])
countries = ['India','Italy', 'US', 'France', 'China']
df = df[df['Country'].isin(countries)]

# Section 3 - Creating a Summary Column
df['Cases'] = df[['Confirmed', 'Recovered', 'Deaths']].sum(axis=1)

df = df.pivot(index='Date', columns='Country', values='Cases')
countries = list(df.columns)
covid = df.reset_index('Date')
covid.set_index(['Date'], inplace=True)
covid.columns = countries

# Section 5 - Calculating Rates per 100,000
populations = {'India':37664517, 'Italy': 67802690 , 'US': 330548815, 'France': 65239883, 'China':1438027228}
percapita = covid.copy()
for country in list(percapita.columns):
    percapita[country] = percapita[country]/populations[country]*100000
    new_col = country+'_DAILY'
    df[new_col] = df[country] -df[country].shift(1)


## US State data
df_s = pd.read_csv('https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv', parse_dates=['date'])
states = ['Oregon','Washington', 'New York', 'New Jersey', 'Louisiana']
df_s = df_s[df_s['state'].isin(states)]

df_s = df_s.pivot(index='date', columns='state', values='cases')

for st in states:
    new_col = st+'_DAILY'
    df_s[new_col] = df_s[st] -df_s[st].shift(1)
