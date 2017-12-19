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
    "github.com/fabioberger/coinbase-go"
)

func main() {
    fmt.Println("Starting the application...")

    c := coinbase.ApiKeyClient(os.Getenv("2hSAn1w8iuSXQDf2"), os.Getenv("DruTEo6fc5GfTlsj0LpeMDIn43ss7CNU"))

    response, err := http.Get("https://api.coinbase.com/v2/prices/spot?currency=USD")
    if err != nil {
        fmt.Printf("The HTTP request failed with error %s\n", err)
    } 
    else {

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
    
    fmt.Println("Terminating the application...")
}