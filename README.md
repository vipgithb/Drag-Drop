# Drag-Drop
<!DOCTYPE html>
<html>
<head>
    <style>
        .container {
            width: 100px;
            height: 250px;
            border: 5px solid black;
            padding: 20px;
            float: left;
		margin-right: 20px;
        }

        .item {
		 display: inline-block;
            width: 70px;
            height: 50px;
            background-color: #cccfff;
            margin: 5px;
            padding: 10px;
            cursor: move;
        }

        .success-message {
            margin-top: 20px;
            font-weight: bold;
        }

    </style>
</head>
<body>
	<h1>Drag and Drop</h1>
    <div class="container" id="container1">
        <div class="item" draggable="true">Item 1</div>
        <div class="item" draggable="true">Item 2</div>
        <div class="item" draggable="true">Item 3</div>
    </div>
    <div class="container" id="container2"></div>
    <div class="success-message" id="successMessage"></div>

    <button onclick="resetContainers()">Reset</button>

    <script>
        // Get references to the containers
    var container1 = document.getElementById('container1');
    var container2 = document.getElementById('container2');
    var successMessage = document.getElementById('successMessage');

    // Store the initial state of the first container
    var initialItems = Array.from(container1.children);

    // Add event listeners for the drag events
    container1.addEventListener('dragstart', dragStart);
    container2.addEventListener('dragover', dragOver);
    container2.addEventListener('drop', drop);

    // Function to handle the dragstart event
    function dragStart(e) {
      // Add a "dragging" class to the dragged item
      e.target.classList.add('dragging');
    }

    // Function to handle the dragover event
    function dragOver(e) {
      // Prevent the default behavior to allow dropping
      e.preventDefault();
    }

    // Function to handle the drop event
    function drop(e) {
      // Remove the "dragging" class from the dropped item
      var draggedItem = document.querySelector('.dragging');
      draggedItem.classList.remove('dragging');

      // Append the dropped item to the second container
      container2.appendChild(draggedItem);

      // Show a success message
      successMessage.textContent = 'Item dropped successfully!';
    }

    // Function to reset the containers to their original state
    function resetContainers() {
      // Remove all items from the second container
      while (container2.firstChild) {
        container2.firstChild.remove();
      }

      // Reset the first container
      container1.innerHTML = '';
      
      // Append copies of the initial items to the first container
      initialItems.forEach(function(item) {
        var itemCopy = item.cloneNode(true);
        container1.appendChild(itemCopy);
      });

      // Clear the success message
      successMessage.textContent = '';
    }
    </script>
</body>
</html>
