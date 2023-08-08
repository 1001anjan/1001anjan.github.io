---
layout: default
title: SpringBoot Example
parent: Elastic Search
nav_order: 3
---
### Simple SpringBoot example
`application.properties`
```yml
spring.data.elasticsearch.cluster-nodes=localhost:9200
#spring.data.elasticsearch.cluster-name=elasticsearch
#spring.data.elasticsearch.properties.user=elastic
#spring.data.elasticsearch.properties.password=ohJaaUChs0DXF6gWVmuh
```
`build.gradle`
```groovy
plugins {
	id 'java'
	id 'org.springframework.boot' version '3.1.2'
	id 'io.spring.dependency-management' version '1.1.2'
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'

java {
	sourceCompatibility = '17'
}

repositories {
	mavenCentral()
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-data-elasticsearch'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
}

tasks.named('test') {
	useJUnitPlatform()
}

```
`ElasticSearchApplication.java`
```java
package com.example.elasticSearch;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.data.elasticsearch.repository.config.EnableElasticsearchRepositories;

@SpringBootApplication
@EnableElasticsearchRepositories
public class ElasticSearchApplication {

	public static void main(String[] args) {
		SpringApplication.run(ElasticSearchApplication.class, args);
	}

}
```
`Book.java`
```java
package com.example.elasticSearch.entity;

import org.springframework.data.annotation.Id;
import org.springframework.data.elasticsearch.annotations.Document;

@Document(indexName = "books")
public class Book {
    @Id
    private String id;
    private String title;
    private String author;
    private int year;

    public int getYear() {
        return year;
    }

    public void setYear(int year) {
        this.year = year;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }
}
```
`BookRepository.java`
```java
package com.example.elasticSearch.repository;

import com.example.elasticSearch.entity.Book;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.data.elasticsearch.repository.ElasticsearchRepository;

import java.util.List;

public interface BookRepository extends ElasticsearchRepository<Book, String> {

    Page<Book> findByAuthor(String author, Pageable pageable);

    List<Book> findByTitle(String title);
}

```
`BookService.java`
```java
package com.example.elasticSearch.service;
import com.example.elasticSearch.entity.Book;
import com.example.elasticSearch.repository.BookRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.PageRequest;
import org.springframework.data.domain.Pageable;
import org.springframework.data.domain.Sort;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class BookService {

    private final BookRepository bookRepository;

    @Autowired
    public BookService(BookRepository bookRepository) {
        this.bookRepository = bookRepository;
    }

    public Book saveBook(Book book) {
        return bookRepository.save(book);
    }

    public Iterable<Book> getAllBooks() {
        return bookRepository.findAll();
    }

    public Book getBookById(String id) {
        return bookRepository.findById(id).orElse(null);
    }

    public void deleteBookById(String id) {
        bookRepository.deleteById(id);
    }

    public Page<Book> findByAuthor(String author, int pageNo, int size) {
        Pageable pageRequest = PageRequest.of(pageNo, size);
        return bookRepository.findByAuthor(author, pageRequest);
    }
    public List<Book> findByTitle(String title) {
        return bookRepository.findByTitle(title);
    }
}
```
`BookController.java`
```java
package com.example.elasticSearch.controller;
import com.example.elasticSearch.entity.Book;
import com.example.elasticSearch.service.BookService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/books")
public class BookController {

    private final BookService bookService;

    @Autowired
    public BookController(BookService bookService) {
        this.bookService = bookService;
    }

    @PostMapping
    public Book createBook(@RequestBody Book book) {
        return bookService.saveBook(book);
    }

    @GetMapping
    public Iterable<Book> getAllBooks() {
        return bookService.getAllBooks();
    }

    @GetMapping("/{id}")
    public Book getBookById(@PathVariable String id) {
        return bookService.getBookById(id);
    }

    @DeleteMapping("/{id}")
    public void deleteBookById(@PathVariable String id) {
        bookService.deleteBookById(id);
    }

    @GetMapping("/text")
    public Iterable<Book> searchByFieldText(@RequestParam String field, @RequestParam String text) {
        return bookService.findByTitle(text);
    }

    @GetMapping("/author")
    public Iterable<Book> searchByAuther( @RequestParam String text) {
        return bookService.findByAuthor(text, 0, 10);
    }
}

```
---


