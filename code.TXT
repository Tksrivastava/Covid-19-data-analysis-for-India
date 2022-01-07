import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Creating a dataframe for world covid-19 data ----
world_df = pd.read_csv('C:/Users/TANUL/PycharmProjects/covidDataAnalysis/owid-covid-data.csv')

# Extracting and saving dataframe for India ---
India_index = world_df[world_df['location'] == 'India'].index  # for creating index for india
India_df = world_df.loc[India_index, ['date', 'total_cases', 'new_cases', 'total_deaths', 'new_deaths',
                                      'total_cases_per_million',
                                      'new_cases_per_million', 'total_deaths_per_million', 'new_deaths_per_million',
                                      'new_tests', 'total_tests',
                                      'total_tests_per_thousand', 'new_tests_per_thousand', 'total_vaccinations',
                                      'people_vaccinated', 'people_fully_vaccinated', 'total_boosters',
                                      'new_vaccinations', 'total_vaccinations_per_hundred',
                                      'people_vaccinated_per_hundred',
                                      'people_fully_vaccinated_per_hundred', 'total_boosters_per_hundred',
                                      'new_vaccinations_smoothed_per_million', 'population', 'population_density',
                                      'aged_65_older', 'aged_70_older', 'median_age']]
India_df.set_index('date', inplace=True)  # Setting date as index
India_df.to_csv('India_covid.csv')

# Comparison of new cases india with respect to moving average new cases of india ----
plt.xlabel('Date', fontweight='bold')
plt.ylabel('Covid-19 cases', fontweight='bold')
plt.title('combine plot of New_covid-19_Cases & Rolling_Average_of_Cases', fontweight='bold')
plt.plot(India_df['new_cases'], 'r', label='New_covid-19_Cases')
plt.plot(India_df['new_cases'].rolling(60).mean(), 'b', label='Rolling_Average_of_Cases')
plt.legend()
plt.grid()
plt.show()

# Covid-19 spreading rate in india ----
plt.xlabel('Date')
plt.ylabel('Every day New Cases with respect to the Total Cases')
plt.title('covid-19 spreading rate', fontweight='bold')
plt.plot((India_df['new_cases']/India_df['total_cases'])*100)
plt.grid()
plt.show()

# Death-rate ----
plt.plot((India_df['new_deaths']/India_df['total_deaths'])*100)
plt.xlabel('Date')
plt.ylabel('Every day New Death Cases with respect to the Total Death Cases')
plt.title('Death rate', fontweight='bold')
plt.grid()
plt.show()

# Lockdown period data
lockdown_India_df = India_df['2020-03-25': '2020-05-31']

# Comparison of new cases india with respect to moving average new cases of india during lockdown period ----
plt.xlabel('Date', fontweight='bold')
plt.ylabel('Covid-19 cases', fontweight='bold')
plt.title('combine plot of New_covid-19_Cases & Rolling_Average_of_Cases during lockdown period', fontweight='bold')
plt.plot(lockdown_India_df['new_cases'], 'r', label='New_covid-19_Cases')
plt.plot(lockdown_India_df['new_cases'].rolling(5).mean(), 'b', label='Rolling_Average_of_Cases')
plt.legend()
plt.grid()
plt.show()

# Death-rate during lockdown period---
plt.plot((lockdown_India_df['new_deaths']/lockdown_India_df['total_deaths'])*100)
plt.xlabel('Date')
plt.ylabel('Every day New Death Cases with respect to the Total Death Cases')
plt.title('Death rate during lockdown period', fontweight='bold')
plt.grid()
plt.show()

# covid-19 spreading rate during lockdown period ----
plt.xlabel('Date')
plt.ylabel('Every day New Cases with respect to the Total Cases')
plt.title('covid-19 spreading rate during lockdown period', fontweight='bold')
plt.plot((lockdown_India_df['new_cases']/lockdown_India_df['total_cases'])*100)
plt.grid()
plt.show()

# heatmap of india's covid-19 data
sns.heatmap(India_df.corr())
plt.show()