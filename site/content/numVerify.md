---
title: "numVerify"
date: 2017-12-18T13:38:17-05:00
draft: false
---

package main

import (
	"encoding/json"
	"fmt"
    "io/ioutil"
	"log"
	"os"
	"net/http"
	"net/url"
)

type Numverify struct {
	Valid               bool   `json:"valid"`
	Number              string `json:"number"`
	LocalFormat         string `json:"local_format"`
	InternationalFormat string `json:"international_format"`
	CountryPrefix       string `json:"country_prefix"`
	CountryCode         string `json:"country_code"`
	CountryName         string `json:"country_name"`
	Location            string `json:"location"`
	Carrier             string `json:"carrier"`
	LineType            string `json:"line_type"`
}

type Response struct {
	Valid               bool   `json:"valid"`
	Number              string `json:"number"`
	LocalFormat         string `json:"local_format"`
	InternationalFormat string `json:"international_format"`
	CountryPrefix       string `json:"country_prefix"`
	CountryCode         string `json:"country_code"`
	CountryName         string `json:"country_name"`
	Location            string `json:"location"`
	Carrier             string `json:"carrier"`
	LineType            string `json:"line_type"`
}

func main() {
	phone := "15712760612"
	safePhone := url.QueryEscape(phone)
	url := fmt.Sprintf("http://apilayer.net/api/validate?access_key=32c85000e678256ddc0c6210fe01f966&number=15712760612", safePhone)
    response, err := http.Get(http://apilayer.net/api/validate?access_key=32c85000e678256ddc0c6210fe01f966&number=15712760612)
	if err != nil {
		fmt.Print(err.Error())
        os.Exit(1)
	}
    responseData, err := ioutil.ReadAll(response.Body)
    var responseObject Response
    json.Unmarshal(responseData, &responseObject)
    fmt.Println(responseObject)
    for i := 0; i < len(responseObject.Numverify); i++ {
		fmt.Println(responseObject.Numverify[i])
	}
	// For control over HTTP client headers,
	// redirect policy, and other settings,
	// create a Client
	// A Client is an HTTP client
	client := &http.Client{}
	// Send the request via a client
	// Do sends an HTTP request and
	// returns an HTTP response
	resp, err := client.Do(req)
	if err != nil {
		log.Fatal("Do: ", err)
		return
	}
	// Callers should close resp.Body
	// when done reading from it
	// Defer the closing of the body
	defer resp.Body.Close()
	// Fill the record with the data from the JSON
	var record Numverify
	// Use json.Decode for reading streams of JSON data
	if err := json.NewDecoder(resp.Body).Decode(&record); err != nil {
		log.Println(err)
	}
	fmt.Println("Phone No. = ", record.InternationalFormat)
	fmt.Println("Country   = ", record.CountryName)
	fmt.Println("Location  = ", record.Location)
	fmt.Println("Carrier   = ", record.Carrier)
	fmt.Println("LineType  = ", record.LineType)

}