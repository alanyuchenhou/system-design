# Features
```gherkin
Feature: Create text
    Scenario: Share text
        Given I'm on home page 
        And I have entered some text
        When I click share
        Then I should see a URL to share
    Scenario: Share text with expiration date
    Scenario: Share text with custom URL
Feature: Read text
    Scenario: Retrieve text using URL
        Given I have shared certain text under certain URL
        When I visit the URL
        Then I should see the text
```

# Object store
```typescript
interface Text {
    key: string;
    body: string;
    createdOn: Date;
    expireDate: Date;
}
```

# Services
```typescript
const HOST = 'pastebin.com/'

interface CreateTextRequest {
    text: string;
    url?: string;
    expireDate?: Date;
}

interface CreateTextResponse {
    url: string;
}

function createText(request: CreateTextRequest): CreateTextResponse {
    const id = uuid()
    const result = this.store.add({
        key: id,
        body: request.text,
        expireDate: request.expireDate,
        })
    return {url: HOST+id}
}

interface ReadTextRequest {
    url: string;
}

interface ReadTextResponse {
    text: string;
}

function readText(request: ReadTextRequest): ReadTextResponse {
    const id = request.url.slice(HOST.length)
    const result = this.store.select({key: id})
    return {text: result.text}
}
```

# Cost
quantity | average | limit
-|-|-
text size | 1 KB | 1 MB
Create text / day | 1 million | NA
new storage / day | 1 GB | NA
Read text / day | 10 million | NA
expiration day | 100 days | 1000 days
