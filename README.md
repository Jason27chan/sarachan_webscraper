# sarachan_webscraper

```python
import requests
import csv

year = 2020
month = 12
api_key = 'iX6BLPr0XnMd5omy4nSNuLIdf4LWO3tX'
url = 'https://api.nytimes.com/svc/archive/v1/{year}/{month}.json?api-key={api_key}'.format(year=year, month=month,api_key=api_key)
response = requests.get(url)

docs = response.json().get('response').get('docs')
with open('times_2020December.csv', 'w', newline='') as csvfile:
    timeswriter = csv.writer(csvfile, delimiter=',',
                            quotechar='"', escapechar='/')
    timeswriter.writerow(['Date', 'Abstract', 'Headline', 'Section'])
    for doc in docs:
        timeswriter.writerow([doc['pub_date'], doc['abstract'], doc['headline']['main'].replace('\'', '/\''), doc['section_name']])
    print('done')

```
