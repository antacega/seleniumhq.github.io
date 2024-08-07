https://web.grindr.com/browser--


from selenium import webdriver
from selenium.webdriver.chrome.options import Options
from bs4 import BeautifulSoup

def extract_grindr_profiles(url):   1. github.com github.com
    """Extrai informações de perfis do Grindr Web (hipotético)."""

    options = Options()
    options.add_argument('--headless=new') 
    driver = webdriver.Chrome(options=options)

    try:
        driver.get(url)
        driver.implicitly_wait(10) 

        page_source = driver.page_source
        soup = BeautifulSoup(page_source, 'html.parser')

        profiles = soup.find_all('div', class_='profile-card') 

        data = []
        for profile in profiles:
            name = profile.find('h3', class_='profile-name').text.strip()
            age = profile.find('span', class_='profile-age').text.strip()
            location = profile.find('span', class_='profile-location').text.strip()

            data.append({
                'name': name,
                'age': age,
                'location': location,
            })

        return data
    
    finally:
        driver.quit()

if __name__ == "__main__":
    url = 'https://web.grindr.com/browse'

    try:
        profiles = extract_grindr_profiles(url)
        for profile in profiles:
            print(profile)
    except Exception as e:
        print(f"Erro ao extrair dados: {e}")
