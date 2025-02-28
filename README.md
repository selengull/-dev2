import requests

api_key = "a73ef63cef90476d861b27139d4e56da"
url = "https://newsapi.org/v2/top-headlines"
params = {
    'country': 'tr',  
    'apiKey': api_key
}

response = requests.get(url, params=params)

if response.status_code == 200:
    data = response.json()
    

    if 'articles' in data:
        articles = data['articles']
        
        if not articles:
            print("Haber bulunamadı.")
        else:
            for article in articles:
                title = article.get('title', 'Başlık yok')
                published_at = article.get('publishedAt', 'Tarih yok')
                source = article.get('source', {}).get('name', 'Kaynak yok')
                link = article.get('url', 'Link yok')

                print(f"Başlık: {title}")
                print(f"Yayın Tarihi: {published_at}")
                print(f"Kaynak: {source}")
                print(f"Link: {link}")
                print("=" * 50) 
    else:
        print("Yanıt formatı beklenildiği gibi değil.")
else:
    print(f"Hata: {response.status_code} - {response.text}")  
