# Solution

### Name: - Sunil Kumar Beniwal<br/>
### Registration No: - 12018959<br/>
### College: - Lovely professional University<br/>
### Assignment Domain: - Frontend Assignment<br/>

### `Problem 1: Explain what the simple List component does.`
The Simple List Component is a React Component which takes an array of items as a prop and renders an unordered list of those items with the option to select a single item from the list.
Upon selection, the background color of the selected list item is set to green, to indicate current selection. The Simple List Component has two components namely WrappedSingleListItem and WrappedListComponent.

### `Problem 2: What problems / warnings are there with code?`
There is a warning and an error found in code.

Warning: 

Line 31:6:  React Hook useEffect has a missing dependency: `setSelectedIndex`. in variable `selectedIndex` under `WrappedListComponent` it must be `useState(null)` instead of `useState()`

In `SingleListItem` component, the `isSelected` prop type should be `PropTypes.bool.isRequired` instead of `PropTypes.bool`. This is because the prop is required and its value should always be a boolean.

Error:

there is an error in Line 54 under it shoud be corrected as `PropTypes.shape` instead of `PropTypes.shapeOf` as property `shapeOf` does not exist in type `propType`

### `Problem 3: Fixed code`


```
import React, { useState, useEffect, memo } from "react";
import PropTypes from "prop-types";

// Single List Item
const WrappedSingleListItem = ({ index, isSelected, onClickHandler, text }) => {
  return (
    <li
      style={{ backgroundColor: isSelected ? "green" : "red" }}
      onClick={() => onClickHandler(index)}
    >
      {text}
    </li>
  );
};

WrappedSingleListItem.propTypes = {
  index: PropTypes.number,
  isSelected: PropTypes.bool,
  onClickHandler: PropTypes.func.isRequired,
  text: PropTypes.string.isRequired,
};

const SingleListItem = memo(WrappedSingleListItem);

// List Component
const WrappedListComponent = ({ items }) => {
  const [selectedIndex, setSelectedIndex] = useState();

  useEffect(() => {
    setSelectedIndex(null);
  }, [items]);

  const handleClick = (index) => {
    setSelectedIndex(index);
  };

  return (
    <ul style={{ textAlign: "left" }}>
      {items ? (
        items.map((item, index) => (
          <SingleListItem
            key={index}
            onClickHandler={() => handleClick(index)}
            text={item.text}
            index={index}
            isSelected={selectedIndex === index}
          />
        ))
      ) : (
        <div>Welcome</div>
      )}
    </ul>
  );
};

WrappedListComponent.propTypes = {
  items: PropTypes.arrayOf(
    PropTypes.shape({
      text: PropTypes.string.isRequired,
    })
  ),
};

WrappedListComponent.defaultProps = {
  items: [
    { text: "My name is Sunil Kumar Beniwal" },
    { text: "I am a Front-end web developer" },
    { text: "Thank You for your consideration" },
    { text: "I will do my best" },
  ],
};

const List = memo(WrappedListComponent);

export default List;
```
