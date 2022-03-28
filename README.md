
1. Corona Opgave
2. Fik lavet opgave 2,3,4(Mangler lidt på 4)
3. Opsætningen er som ses nedenfor med div. imports og ellers køre man det bare i jupyter.




import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
from sklearn.datasets import make_blobs
df = pd.read_csv(
    '/home/jovyan/my_notebook/owid-covid-data.csv')



#Opgave 2: Hvilket land i europa har testet flest personer pr. tusinde indbyggere (total_tests_per_thousand), siden juli 2021 til nu?
print("Opgave 2")
mask = df['continent'] == 'Europe'
max_cases = df[mask].groupby('location').agg({'total_tests_per_thousand': [
    'max']})
print(max_cases.sort_values([('total_tests_per_thousand', 'max')], ascending=False))
print("")
print("")
print("")


#Opgave 3 Vis en graph af de ti lande med flest døde til dags dato.
print("Opgave 3")
top_10_most = df[df['continent'].notna()].groupby('location').agg({'total_cases': [
    'max']}).sort_values([('total_cases', 'max')], ascending=False).head(10)
#Tester##top_10_dataframe = df[df['continent'].notna()].groupby('location')['total_cases'].agg('max')
print(top_10_most)
print(top_10_most.columns)

#ages = list(top_10_most.keys())
top_10_most.plot()
#plt.show()
#top_10_most.plot.scatter(x = 0, y = 1)
#plt.plot(top_10_most)
#plt.plot(top_10_most)


#Opgave 4. Vælg tre lande og vis udviklingen af døde i forhold til total antal smittede i procent fra d. 1 april 2020 til dags dato."
KOR = df[df.iso_code == 'KOR']
#USA = df[df.iso_code == 'USA']

def plot_case(data,country_name):
    #test = plt.subplots()
    #fig = test,(specs=[[{'secondary_y':True}]])
    
   new_data = pd.DataFrame({'date':data.date,'total_cases':data.total_cases_per_million,'new_cases':data.new_cases_per_million})
   df = pd.DataFrame(new_data,columns=['date','total_cases'])
   df.plot(x ='date', y='total_cases', kind = 'scatter')
   plt.show()
   plot_case(KOR,'KOREA')
