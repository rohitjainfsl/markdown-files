<!-- How to create a custom Hook (show starting animation from prism)

A custom hook is a function which starts with the word 'use'.
A custom hook can incorporate state, sideeffects and other logics using standard hooks -->


import { useState, useEffect } from 'react';

function useWindowSize() {
  const [width, setWidth] = useState(window.innerWidth);
  const [height, setHeight] = useState(window.innerHeight);

  useEffect(() => {
    function handleResize() {
      setWidth(window.innerWidth);
      setHeight(window.innerHeight);
    }

    window.addEventListener('resize', handleResize);

    return () => {
      window.removeEventListener('resize', handleResize);
    };
  }, []);

  return { width, height };
}


<!-- To use this custom hook in a component, you simply call it from within your component's code: -->

<!-- import React from 'react';
import useWindowSize from './useWindowSize';

function WindowSizeDisplay() {
  const { width, height } = useWindowSize();

  return (
    <div>
      Window size: {width} x {height}
    </div>
  );
}

export default WindowSizeDisplay; -->


<!-- Now, you can use the WindowSizeDisplay component anywhere in your application and it will display the current window size, without having to write the logic to track the window size multiple times. -->





<!-- A more complex example -->

import { useState, useEffect } from 'react';

function useDebouncedSearch(search, delay) {
  const [debouncedSearch, setDebouncedSearch] = useState(search);

  useEffect(() => {
    let timeoutId = null;

    if (debouncedSearch !== search) {
      clearTimeout(timeoutId);
      timeoutId = setTimeout(() => {
        setDebouncedSearch(search);
      }, delay);
    }

    return () => {
      clearTimeout(timeoutId);
    };
  }, [search, delay, debouncedSearch]);

  return debouncedSearch;
}


<!-- Here's how you would use this custom hook in a component: -->

import React, { useState } from 'react';
import useDebouncedSearch from './useDebouncedSearch';

function SearchInput({ onSearch }) {
  const [search, setSearch] = useState('');
  const debouncedSearch = useDebouncedSearch(search, 500);

  useEffect(() => {
    onSearch(debouncedSearch);
  }, [debouncedSearch, onSearch]);

  return (
    <input
      type="text"
      value={search}
      onChange={(e) => setSearch(e.target.value)}
    />
  );
}

export default SearchInput;


<!-- With this custom hook, you can avoid making too many search requests to your API while the user is still typing, because the search will only be performed once the user has stopped typing for 500 milliseconds. -->