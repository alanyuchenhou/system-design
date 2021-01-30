# What is pastebin
A web service that stores and shares text(or image)

# Requirements
```gherkin
Feature: Create text
    Scenario: Enter text and get URL
        Given I'm on home page
        When I enter text
        And I click share
        Then I should see a URL to share
Feature: Read text
    Scenario: Retrieve text using URL
        When I visit the previously generated URL
        Then I should see the text I previously stored
```
# Design considerations

# Capacity estimation and constraints
| Feature | Daily usage | Daily storage growth |
|-|-|-|
| Create text | 1 million | 1 GB |
| Read text | 1 billion | NA |

# System APIs
```protobuf
message CreateRequest = {
    required string content;
}
```

# Diagram
```yuml
// {type:class}
// {direction:topDown}
[note: You can stick notes on diagrams too!{bg:cornsilk}]
[Customer]<>1-orders 0..*>[Order]
[Order]++*-*>[LineItem]
[Order]-1>[DeliveryMethod]
[Order]*-*>[Product|EAN_Code|promo_price()]
[Category]<->[Product]
[DeliveryMethod]^[National]
```
