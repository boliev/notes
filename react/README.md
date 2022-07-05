https://www.educative.io/courses/react-beginner-to-advanced

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <title>Hello React!</title>
    </head>
    <body>
        <div id="root"></div>
        <script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script>
        <script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>
        <script>
            // Placeholder for our first component
            class HelloWorld extends React.Component {
                render() {
                    return React.createElement('div', { id: 'hello-world' }, 'Hello World');
                }
            }
            ReactDOM.render(React.createElement(HelloWorld), document.getElementById('root'))
        </script>
    </body>
</html>
```

As you can see, we get an empty page with the given code because there was nothing inside the div tag. This div will be used as our mount node to show our first React component.

