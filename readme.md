# Test Cases for POST /pet Endpoint

## Positive Test Cases

### TC001 - Successful pet creation with minimal required fields

**Precondition:** API is available  
**Steps:**

1. Send POST request with body containing:
   - id (integer)
   - name (string)
   - photoUrls (array)
   - status = "available"

**Expected Result:**

- Status code: 200
- Response contains created pet
- All submitted data is saved correctly

### TC002 - Create pet with all possible fields

**Precondition:** API is available  
**Steps:**

1. Send POST request with full set of fields:
   - id
   - category (object with id and name)
   - name
   - photoUrls (array of URLs)
   - tags (array of objects with id and name)
   - status

**Expected Result:**

- Status code: 200
- All fields are saved and returned in response
- Response structure matches specification

### TC003 - Create pet with long field values

**Precondition:** API is available  
**Steps:**

1. Send POST request with:
   - name (255 characters)
   - photoUrls (array of 50 URLs)
   - tags (20 tags)

**Expected Result:**

- Status code: 200
- Data successfully saved without truncation

### TC004 - Create pet with special characters in name

**Precondition:** API is available  
**Steps:**

1. Send POST request with name containing special characters (@#$%^&*()_+)

**Expected Result:**

- Status code: 200
- Name saved without changes

## Negative Test Cases

### TC005 - Attempt to create pet without required fields

**Precondition:** API is available  
**Steps:**

1. Send POST request without name field

**Expected Result:**

- Status code: 400
- Validation error message

### TC006 - Create pet with incorrect data types

**Precondition:** API is available  
**Steps:**

1. Send POST request with:
   - id: "string" instead of number
   - photoUrls: string instead of array

**Expected Result:**

- Status code: 400
- Invalid data format message

### TC007 - Create pet with invalid status

**Precondition:** API is available  
**Steps:**

1. Send POST request with status = "invalid_status"

**Expected Result:**

- Status code: 400
- Invalid status value message

### TC008 - Attempt to create pet with duplicate ID

**Precondition:**

- API is available
- Pet with specific ID already exists

**Steps:**

1. Send POST request with existing ID

**Expected Result:**

- Appropriate duplicate handling (update or error)
- Clear result message

### TC009 - Check request size limits

**Precondition:** API is available  

**Steps:**

1. Send POST request with:
   - name (>1000 characters)
   - photoUrls (>100 URLs)
   - tags (>100 tags)

**Expected Result:**

- Appropriate handling of oversized request
- Status code: 413 or similar

### TC010 - Verify error handling for invalid category

**Precondition:**

- API is available
- Category with specific ID does not exist

**Steps:**

1. Send POST request with a category ID that does not exist

**Expected Result:**

- Status code: 400
- Clear error message indicating the category does not exist
