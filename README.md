This repo contains test cases in postman.

These tests validate Trello apis.

**1.reusable function to go through the array index without hardcoding**

```
function _isContains(json, keyname, value) {
    return Object.keys(json).some(key => {
        return typeof json[key] === 'object' && json[key] !== null ? 
        _isContains(json[key], keyname, value) : key === keyname && json[key] === value;
    });
}
```

**2.Check the names of the board is as per your expectation**
checking name is Board2

pm.test("The response contains a valid id in the response", function () {
    var jsonData=pm.response.json();
    pm.expect(_isContains(jsonData, "name" ,"Board2")).to.be.true;
});

**3. Negative scenaro, invalid board name:**

pm.test("The response contains a invalid id in the response", function () {
    var jsonData=pm.response.json();
    pm.expect(_isContains(jsonData, "name" ,"Board")).to.be.true;
});

**4.Save the board Ids in collection Variable.**

let board_ids = []
_.each(pm.response.json(), (el) => board_ids.push(el.id))

pm.globals.set("board_ids", JSON.stringify(board_ids));
