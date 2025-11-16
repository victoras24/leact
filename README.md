# leact - trying to master react as junior dev

I have little bit less than a year of working experience in React, but always I feel that I have knowledge gaps on how React works. Especially when it comes to hooks like, useCallback, useMemo, useRef. I know the reason why we use each one but it seems like I have a difficulty on using them on my code. They usually appear when an LLM suggest me to do. So I have decided to start from the basics and document my progress, difficulties that I found and if eventually I have learned anything. After the comlpetion of the websocket server from scratch with C#, I learned a lot about network programming and how the server and client communicate. I even learned how to read and deconstruct a frame, which is very interesting. My goal was to just understand how the websockets are working, I knew from a high perspective how they work, but I didn't really understand what is happening behind the scenes. So digging lower it really benefited me on understanding how the websockets work. The same goal I have with this project. Instead of jumping into a project and just code my way to the end result, or to just complete a ticket, create a feature, without really getting some knowledge, I decided to go deep and document each step.

Starting from just an html file and inline import the React into the project, instead of just executing a command and just magic, boom, you got everything ready to code. Trust me, if you are a junior developer I think there is a probability that you don't know how to connect the css file with the html file. I'm not saying by any means that it's essential to know, you can just google it and find it within a minute. But isn't that showing we don't dig enough to understand how the code works. I think that's the problem with the gaps in my knowledge. We depend a lot on the LLMs, without understanding the basics. Just propmt your way into the solution. But if you stuck on a harder task? If you need to debug? But you don't have the idea how it works? Then you just depend on your senior or a lucky prompt to rescue you. To be honest I'm using LLMs to finish a lot of tickets in my work and I do it because of the time pressure, or maybe I'm the problem and I'm slow. Maybe. But the point it that I'm not getting the satisfaction. The satisfaction of solving a problem and having the aha moment. Even on the harded tasks, if I use the help of an LLM I don't get the satisfaction. So I started using it just like google and adding the phrase "Don't code". I want to give me the steps on how I can find the solution. Maybe also that is the problem. I'm not thinking on the path to find the solution, which maybe is necessary to solve hard problems. Anyway let's continue. That's something that I can analyze on a different project.

Created the html file, added the necessary tags. Like html, head, body, script. And now? We have to somehow start scripting I guess. So I new the way to do that just started with an easy console log in the script tags. Now we need to render a component on the page. So I did the below

    <body>
    	<script>
    		function App() {
    			var count;

    			return (
    				<div>
    					<p>{count}</p>
    					<button onClick={() => console.log(count)}>
    						click me
    					</button>
    				</div>
    			);
    		}
            App();
    	</script>
    </body>

Guess what. Nothing get's displayed. Why? I though that just by returning the div, it would be displayed on the page. Yeah it didn't. So started searching and found that I need to install react-dom. React-dom we need it to render the components to the page! That's what we are missing right now. So I will need to create a div add the attribute id and name it root or whatever. Then we need to use the createRoot function that will return an object where inside that object is the render method. In that method we need to pass the component that we want to render into the page. Okay let's refresh aaand still we got errors. Why?

Because we have JSX and in order to use JSX we need React. So let's inline import react using cdn. Aaand still nothing. So I continue searching I find that browser cannot read JSX, so we need something to compile to js and that is babel. Let's inline import babel also and don't forget to add the type attribute into script tag type="text/babel", otherwise it cannot find what to compile. Here is the end result:

    <!DOCTYPE html>
    <html>
        <header>
            <title>Mastering React</title>
            <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
            <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
            <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
        </header>

        <body>
            <div id="root"></div>
            <script type="text/babel">
                function App() {
                    const [count, setCount] = React.useState(0);

                    return (
                        <div>
                            <p>{count}</p>
                            <button onClick={() => setCount((prevCount) => ++prevCount)}>
                                click me
                            </button>
                        </div>
                    );
                }
                const rootDomNode = document.getElementById("root");
                const root = ReactDOM.createRoot(rootDomNode);
                root.render(<App />);
            </script>
        </body>
    </html>
