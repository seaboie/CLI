<a id="readme-top"></a>


<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="">
    <img src="https://raw.githubusercontent.com/seaboie/images/main/images/logoTransparent.png" alt="Logo" width="120" height="120">
  </a>

  <h3 align="center">CLI</h3>

  <p align="center">
    Command line
    
  </p>

</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary style='font-size: 2em;'>Table of Contents</summary>
  <ol style='font-size: 1.5em;'>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#curl">Curl</a></li>
    <li><a href="#curl--quicktype---convert-api-response-to-typescript-type">Curl & Quicktype ( Convert API response to typescript Type</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>




<!-- GETTING STARTED -->
## Getting Started


### Prerequisites



### Installation



<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage


## Curl  

To format JSON nicely in the terminal, you can use tools like `jq`, which is a lightweight and flexible command-line JSON processor. If you have `jq` installed, you can use it to format the JSON output from your `curl` command. Here's how you can do it:

1. First, ensure you have `jq` installed. If not, you can install it using a package manager like `apt` for Ubuntu or `brew` for macOS.

2. Use the following command to fetch the JSON data and format it:

```bash
curl -s https://fakestoreapi.com/products | jq
```

This command will pipe the output of the `curl` command to `jq`, which will format the JSON data in a more readable way in your terminal.

If you don't have `jq` installed, you can install it using:

- On Ubuntu/Debian:
  ```bash
  sudo apt-get install jq
  ```

- On macOS (using Homebrew):
  ```bash
  brew install jq
  ```

This should help you view the JSON data in a nicely formatted way.

---  

If you want to log only the first 3 items from the JSON data retrieved using `curl` and formatted with `jq`, you can use the array slicing feature of `jq`. Here's how you can do it:

```bash
curl -s https://fakestoreapi.com/products | jq '.[0:3]'
```

This command will fetch the JSON data from the URL and then use `jq` to slice the array, displaying only the first three items. The `.[0:3]` part is the slicing syntax where `0` is the starting index and `3` is the ending index (exclusive), so it includes items at index 0, 1, and 2.  

---  

If you want to retrieve only the last item from the JSON data using `jq`, you can use negative indexing. Here's how you can modify the command to get the last item:

```bash
curl -s https://fakestoreapi.com/products | jq '.[-1]'
```

In this command, `.[-1]` is used to access the last element in the array. Negative indices in `jq` count from the end of the array, so `-1` refers to the last item, `-2` would refer to the second last item, and so on.  

To log the last two items from the JSON data using `jq`, you can use array slicing with negative indices. Here's how you can do it:

```bash
curl -s https://fakestoreapi.com/products | jq '.[-2:]'
```

In this command, `.[-2:]` is used to slice the array starting from the second last item to the end of the array. This will display the last two items in the JSON data.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Curl & Quicktype :::  `Convert API response to TypeScript Type`

To convert the response from an API link (like a REST API returning JSON) into a TypeScript type and save it as a `.ts` file, you can use a combination of command-line tools like `curl` or `wget`, and a package like [`quicktype`](https://github.com/quicktype/quicktype).

---

### ✅ **1. Install `quicktype` CLI**

```bash
npm install -g quicktype
```

---

### ✅ **2. Convert API response to TypeScript type**

Here’s a command-line one-liner that fetches the API response and generates `type.ts`:

```bash
curl -s "https://api.example.com/data" | quicktype --lang ts --top-level MyType --just-types > type.ts
```

* Replace `https://api.example.com/data` with your API URL.
* Replace `MyType` with the name you want for your main TypeScript interface.
* Output is saved to `type.ts`.

---

### 💡 Example

```bash
curl -s "https://jsonplaceholder.typicode.com/users" | quicktype --lang ts --top-level User --just-types > user.types.ts
```

This will generate a `user.types.ts` file with interfaces based on the API JSON structure.


Let’s break down the command you provided step by step:

```bash
curl -s "https://jsonplaceholder.typicode.com/users" | quicktype --lang ts --top-level User --just-types > user.types.ts
```

### Explanation of the Command

This command fetches JSON data from an API, processes it to generate TypeScript type definitions, and saves the result to a file. Here's a detailed breakdown:

1. **curl -s "https://jsonplaceholder.typicode.com/users"**:
   - `curl` is a command-line tool used to make HTTP requests and fetch data from URLs.
   - The `-s` flag stands for "silent," which suppresses the progress meter and error messages, making the output cleaner.
   - The URL `"https://jsonplaceholder.typicode.com/users"` is a public API endpoint from JSONPlaceholder, a fake REST API for testing and prototyping. This specific endpoint returns a JSON array of user objects, each containing fields like `id`, `name`, `username`, `email`, `address`, `phone`, `website`, and `company`.
   - This part of the command retrieves the JSON data and outputs it to the terminal (stdout).

2. **|** (Pipe Operator):
   - The pipe (`|`) redirects the output of the `curl` command (the JSON data) to the next command, `quicktype`, as its input.

3. **quicktype --lang ts --top-level User --just-types**:
   - `quicktype` is a tool that generates type definitions (or code) from JSON data for various programming languages.
   - `--lang ts`: Specifies that the output should be in TypeScript (`ts`).
   - `--top-level User`: Defines the name of the top-level type in the generated TypeScript code as `User`. Since the JSON data is an array of user objects, `quicktype` will generate a type definition for a single user object named `User`, and the array will be typed as `User[]`.
   - `--just-types`: Instructs `quicktype` to generate only the type definitions (interfaces or types) without additional code like serializers or deserializers.
   - `quicktype` takes the JSON input from `curl` (via the pipe) and infers the structure of the data to create TypeScript interfaces that match the JSON schema.

4. **> user.types.ts**:
   - The `>` operator redirects the output of the `quicktype` command to a file named `user.types.ts`.
   - If the file already exists, this will overwrite it. If you want to append instead, you would use `>>`.

### What Happens When You Run This Command?

1. **Fetch JSON Data**:
   - The `curl` command retrieves a JSON array from `https://jsonplaceholder.typicode.com/users`. The JSON looks something like this (simplified):
     ```json
     [
       {
         "id": 1,
         "name": "Leanne Graham",
         "username": "Bret",
         "email": "Sincere@april.biz",
         "address": {
           "street": "Kulas Light",
           "suite": "Apt. 556",
           "city": "Gwenborough",
           "zipcode": "92998-3874",
           "geo": {
             "lat": "-37.3159",
             "lng": "81.1496"
           }
         },
         "phone": "1-770-736-8031 x56442",
         "website": "hildegard.org",
         "company": {
           "name": "Romaguera-Crona",
           "catchPhrase": "Multi-layered client-server neural-net",
           "bs": "harness real-time e-markets"
         }
       },
       ...
     ]
     ```

2. **Generate TypeScript Types**:
   - `quicktype` processes this JSON and generates TypeScript interfaces that reflect the structure of the data.
   - With `--top-level User`, the top-level type will be named `User`, and since the JSON is an array, the output will represent an array of `User` objects (`User[]`).
   - The `--just-types` flag ensures that only type definitions are generated, not additional code for parsing or serialization.

3. **Save to File**:
   - The generated TypeScript code is saved to `user.types.ts`.

### Example Output in `user.types.ts`

Based on the JSON structure from JSONPlaceholder, the generated `user.types.ts` file would look something like this:

```typescript
export interface User {
    id: number;
    name: string;
    username: string;
    email: string;
    address: Address;
    phone: string;
    website: string;
    company: Company;
}

export interface Address {
    street: string;
    suite: string;
    city: string;
    zipcode: string;
    geo: Geo;
}

export interface Geo {
    lat: string;
    lng: string;
}

export interface Company {
    name: string;
    catchPhrase: string;
    bs: string;
}
```

- Each interface corresponds to a nested object in the JSON structure.
- The top-level type is `User`, as specified by `--top-level User`.
- Since the JSON is an array, you would typically use `User[]` when importing and using this type in your TypeScript code.

### Purpose of This Command

This command is useful for quickly generating TypeScript type definitions from a JSON API response. By piping the JSON data directly from `curl` to `quicktype`, you automate the process of creating type-safe interfaces for use in a TypeScript project. This ensures that your code can work with the API data in a strongly typed manner, reducing errors and improving development efficiency.

### Prerequisites

To run this command successfully, you need:
- `curl` installed on your system (available by default on most Unix-like systems or can be installed on Windows).
- `quicktype` installed globally via npm (`npm install -g quicktype`).
- A working internet connection to fetch the JSON from the JSONPlaceholder API.

### Potential Variations

- If you want to generate types for a different language, you can change `--lang ts` to another supported language, like `--lang python` or `--lang java`.
- If you want additional code (e.g., for JSON serialization), remove the `--just-types` flag.
- If you want to use a local JSON file instead of an API, you can replace the `curl` part with `cat file.json | quicktype ...`.

### Error Handling

- If the API is down or the URL is incorrect, `curl` will fail, and `quicktype` will receive no input, resulting in an error.
- If `quicktype` is not installed, you’ll get a “command not found” error.
- If the output file (`user.types.ts`) cannot be written (e.g., due to permissions), the command will fail.

This command is a powerful example of combining tools to streamline development workflows, particularly for TypeScript developers working with APIs.



<p align="right">(<a href="#readme-top">back to top</a>)</p>

---


<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>




<!-- ACKNOWLEDGMENTS -->
## Acknowledgments  

* [GitHub Emoji Cheat Sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet)



<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[logo-image]:https://raw.githubusercontent.com/seaboie/images/main/images/logoTransparent.png

