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

    response, err := https.get("https://api.coinbase.com/v2/prices/spot?currency=USD")
    
     if err != nil {
        fmt.Printf("The HTTP request failed with error %s\n", err)
    } else {
        data, _ := ioutil.ReadAll(response.Body)
        fmt.Println(string(data))
    }
    
    fmt.Println("Terminating the application...")
}