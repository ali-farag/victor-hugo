---
title: "Bitcoin API"
draft: false
---
package main

import (
    "bytes"
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
)

func main() {
    fmt.Println("Starting the application...")

    c := coinbase.ApiKeyClient(os.Getenv("2hSAn1w8iuSXQDf2"), os.Getenv("DruTEo6fc5GfTlsj0LpeMDIn43ss7CNU"))

    response, err := http.Get("https://api.coinbase.com/v2/prices/spot?currency=USD")
    if err != nil {
        fmt.Printf("The HTTP request failed with error %s\n", err)
    } else {
        data, _ := ioutil.ReadAll(response.Body)
        fmt.Println(string(data))

        fmt.Printf(c)
                
price, err := c.GetBuyPrice(1)
if err != nil {
	log.Fatal(err)
}
fmt.Println(price.Subtotal.Amount) 
// Subtotal does not include fees

fmt.Println(price.Total.Amount)
// Total includes coinbase & bank fee


price, err = c.GetSellPrice(1)
if err != nil {
	log.Fatal(err)
}
fmt.Println(price.Subtotal.Amount) // Subtotal is current market price
// '9.90'
fmt.Println(price.Total.Amount) // Total is amount you will receive (after fees)
// '9.65'



    }
    <!-- jsonData := map[string]string{"firstname": "Ali", "lastname": "Farag"}
    jsonValue, _ := json.Marshal(jsonData)
    response, err = http.Post("https://httpbin.org/post", "application/json", bytes.NewBuffer(jsonValue))
    if err != nil {
        fmt.Printf("The HTTP request failed with error %s\n", err)
    } else {
        data, _ := ioutil.ReadAll(response.Body)
        fmt.Println(string(data))
    } -->
    fmt.Println("Terminating the application...")
}