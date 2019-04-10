## WEBPACK NOTES

### Core Concepts
JavaScript Modules 
- Reuseable
- Encapsulated
- Organized

Webpack is a module bundler. It lets you write modules that work in the browser.
- Webpack CLI - uses Node API behind the scenes

#### How it works?
1. Entry: The first javascript file to load to kick-off your application. Webpack uses this as the starting point to build your graph
- Tells webpack WHAT (files) to load from the browser. It complements the `Output` property
```
module.exports = {
	entry: './browser.main.ts',
	// ...
}
```

2. Output: Tells Webpack WHERE and HOW to distribute budles (compilations). Works with `Entry`
```
	output: {
		path: path.resolve('./dist'),
		filename: './bundle.js'
	}
```

3. Loaders: It tells Webpack HOW to interpret and translate files. They return compilations. A loader is just a function that takes a source and returns a new source!
- Loaders are also js modules (functions) that takes the source file, and returns it in a [modified] state.
```
	module: {
		rules: [
			{
				test: /\.ts$/,
				use: 'ts-loader'
			},
			{
				test: /\.js$/,
				use: 'babel-loader' 
			},
			{
				test: /\.css$/,
				use: 'css-loader'
			},
		]
	}
```

- We can modify and filter through the loaders as well:
```
	rules: [
		{
			test: regex,
			use: (Array|String|Function),
			include: /some_dir_name/, // RegExp[]
			exclude: [/\.(spec|e2e)|.ts$/], // RegExp[]
			issuer: (RegExp|String)[],
			enforce: "pre"|"post"
		}
	]
```
- `test`: A regex that instructs the compiler which files to run the loader against
- `use`: An array/string/function that returns loader objects
- `include`: An array of regex that instructs the compiler which folders/files to include. Will only search paths provided with the include
- `exclude`: An array of regex that instructs the compiler which folders/files to ignore
- `enforce`: Tells webpack to run this rule before or after all other rules

- Chaining Loaders
```
	rules: [
		{
			test: /\.less$/,
			use: ['style-loader', 'css-loader', 'less-loader']
		}
	]
```

4. Plugins: An ES5 Object which implements an `apply` function. The compiler uses it to emit events

https://www.youtube.com/watch?v=gEBUU6QfVzk&t=605s

