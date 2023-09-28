# React useContext

```js
//---------
// App.jsx
//---------
import React from "react";
import FunctionContextComponent from "./FunctionContextComponent";
import { ThemeProvider } from "./ThemeContext";

export default function App() {
  return (
    <div>
      <ThemeProvider>
        <FunctionContextComponent />
      </ThemeProvider>
    </div>
  );
}
//-------------------------------
// FunctionContextComponent.jsx
//-------------------------------
import React from "react";
import { useTheme, useThemeUpdate } from "./ThemeContext";

export default function FunctionContextComponent() {
  const darkTheme = useTheme();
  const toggleTheme = useThemeUpdate();
  // the theme style
  const themeStyles = {
    backgroundColor: darkTheme ? "#333" : "#CCC",
    color: darkTheme ? "#CCC" : "#333",
    padding: "2rem",
    margin: "2rem",
  };
  return (
    <div>
      <button onClick={toggleTheme}>Toggle Theme</button>
      <div style={themeStyles}>FunctionContextComponent</div>
    </div>
  );
}
//-------------------
// ThemeContext.jsx
//-------------------
import React, { useContext, useState } from "react";

const ThemeContext = React.createContext();
const ThemeUpdateContext = React.createContext();

//create a hook to expose into the function component
export function useTheme() {
  return useContext(ThemeContext);
}
//create a hook to expose into the function component
export function useThemeUpdate() {
  return useContext(ThemeUpdateContext);
}

export function ThemeProvider({ children }) {
  const [darkTheme, setDarkTheme] = useState(true);

  function toggleTheme() {
    setDarkTheme((prevDarkTheme) => !prevDarkTheme);
  }

  return (
    <ThemeContext.Provider value={darkTheme}>
      <ThemeUpdateContext.Provider value={toggleTheme}>
        {children}
      </ThemeUpdateContext.Provider>
    </ThemeContext.Provider>
  );
}

```
