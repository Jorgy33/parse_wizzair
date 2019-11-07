from selenium import webdriver
import time
import smtplib


def get_mail():
    server = smtplib.SMTP('smtp.gmail.com', 587)
    server.ehlo()
    server.starttls()
    server.ehlo()
    server.login('ibanez321ex@gmail.com', 'aecashgkotqmyyye')

    subject = 'The price fell down!'
    body = 'Check the WizzAir link https://wizzair.com/#/booking/select-flight/IEV/WAW/2020-02-06/null/1/0/0/0/null'
    cur_price = f'Current price is: {price}'

    msg = f'Subject: {subject}\n\n{body}\n{cur_price}'

    server.sendmail(
        'ibanez321ex@gmail.com',
        'ibanez321ex@gmail.com',
        msg)

    print('EMAIL HAS BEEN SENT')

    server.quit()


starter_price = 1000
while True:
    driver = webdriver.Chrome(executable_path=r'/usr/local/share/chromedriver')
    url = 'https://wizzair.com/#/booking/select-flight/IEV/WAW/2020-02-06/null/1/0/0/0/null'
    driver.get(url)
    time.sleep(45)
    price = driver.find_element_by_xpath('//*[@id="chart-2020-02"]/ul/li[4]/label/div/div/span')
    price = price.text
    price = int(''.join(filter(str.isdigit, price)))
    if price < starter_price:
        get_mail()
        driver.close()
        starter_price = price
        print(f'new price: {price}')
        time.sleep(21600)
        continue

    print(f'same price: {price}')
    driver.close()
    time.sleep(21600)
