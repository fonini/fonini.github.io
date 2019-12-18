---
title: "Validando datas com o go-playground/validator"
date: 2019-12-18 14:25:35 -0300
layout: post
author: fonini
permalink: /2019/12/18/validando-datas-com-o-go-playground-validator/
tags: 
  - golang
---

[Doctrine](http://www.doctrine-project.org)
[Custom Validator](https://godoc.org/github.com/go-playground/validator#hdr-Custom_Validation_Functions) para datas padrão [ISO 8601](https://pt.wikipedia.org/wiki/ISO_8601) para [Go](https://golang.org/), utilizando o pacote [go-playground/validator](https://github.com/go-playground/validator).

{% highlight go %}package main

import (
	"fmt"
	"regexp"

	"gopkg.in/go-playground/validator.v10"
)

func IsISO8601Date(fl validator.FieldLevel) bool {
	regex := "^(-?(?:[1-9][0-9]*)?[0-9]{4})-(1[0-2]|0[1-9])-(3[01]|0[1-9]|[12][0-9])((?:T|\\s)(2[0-3]|[01][0-9]):([0-5][0-9]):([0-5][0-9])?(Z)?)?$"
	ISO8601DateRegex := regexp.MustCompile(regex)

	return ISO8601DateRegex.MatchString(fl.Field().String())
}

type Dates struct {
	ISO8601DateTime string `validate:"ISO8601date"`
	ISO8601Date     string `validate:"ISO8601date"`
	Invalid         string `validate:"ISO8601date"`
}

func main() {
	validator := validator.New()
	validator.RegisterValidation("ISO8601date", IsISO8601Date)

	dates := Dates{ISO8601DateTime: "2019-12-18T14:19:30Z", ISO8601Date: "2019-12-18", Invalid: "2019-60-12"}

	err := validator.Struct(dates)

	if err != nil {
		fmt.Println(err)
	}
}

{% endhighlight %}