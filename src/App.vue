<template>
  <div>
    <h2>Book List</h2>
    <form @submit.prevent="addBook">
      <input type="text" v-model="newBook" placeholder="Enter a new book" />
      <button class="addBook" type="submit">Add</button>
    </form>
    <table>
      <thead>
        <tr>
          <th>Book ID</th>
          <th>Book Text</th>
          <th>Completed</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="book in books" :key="book.id">
          <td>{{ book.id }}</td>
          <td>{{ book.text }}</td>
          <td>
            <p v-if="book.complete">Complete</p>
            <p v-else>Incomplete</p>
          </td>
          <td>
            <button class="completed" @click="toggleCompleted(book.id)" :style="{ backgroundColor: book.completed ? 'green' : 'orange' }">
              {{ book.completed ? 'Complete' : 'Incomplete' }}
            </button>
            <button @click="removeBook(book.id)">Remove</button>
          </td>
        </tr>
      </tbody>
    </table>
    <h4>Total of book that already completed: {{ completedBooksCount }}</h4>
  </div>
</template>

<script>
export default {
  data() {
    return {
      books: [
        { id: 1, text: 'English', completed: true },
        { id: 2, text: 'PHP', completed: false },
        { id: 3, text: 'DB', completed: false }
      ],
      newBook: ''
    };
  },
  computed: {
    completedBooksCount() {
      return this.books.filter(book => book.completed).length;
    }
  },
  methods: {
    addBook() {
      if (this.newBook.trim() !== '') {
        this.books.push({
          id: this.books.length + 1,
          text: this.newBook,
          completed: false
        });
        this.newBook = '';
      }
    },
    removeBook(bookId) {
      this.books = this.books.filter(book => book.id !== bookId);
    },
    toggleCompleted(bookId) {
      this.books = this.books.map(book => {
        if (book.id === bookId) {
          book.completed = !book.completed;
        }
        return book;
      });
    }
  }
};
</script>

<style>
h2 {
  color: #333;
}

input {
  margin-bottom: 10px;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 10px;
}

th, td {
  padding: 10px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

th {
  background-color: #f2f2f2;
}

button {
  padding: 5px 10px;
  background-color: red;
  color: white;
  border: none;
  cursor: pointer;
}

.addBook, .completed {
  background-color: green;
  color: white;
  border: none;
  cursor: pointer;
  margin: 10px;
}
</style>