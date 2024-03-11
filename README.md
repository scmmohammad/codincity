# codincity
Assessment
import requests

def get_user_agent():
    try:
        response = requests.get('https://httpbin.org/user-agent')
        user_agent = response.json()['user-agent']
        return user_agent
    except Exception as e:
        print("Error fetching user agent:", e)
        return None

def main():
    print("Welcome to 2022")
    user_agent = get_user_agent()
    if user_agent:
        print("User Agent:", user_agent)

if __name__ == "__main__":
    main()
