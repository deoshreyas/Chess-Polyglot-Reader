# Chess-Polyglot-Reader
A Chess Opening Book reader that supports Polyglot books of the .bin format. The code is fully documented.

## :star: Features
- Well-documented
- Ability to load and read Polyglot books
- Returns the book moves in a standard format so you can integrate it with your projects (see below)
- Can randomly extract a book move using the zobrist hash of a position
- Can convert a book move to the UCI protocol
- Ability to process and return the move weight and learn values as well
- Everything is in the `Reader::` namespace, so it won't pollute your namespace

## :grey_question: How to use it?
This is a single header library. Just download `reader.hpp` or copy the source code.

## :checkered_flag: How to use the book moves in your project?
The book moves are returned in a single format.
For example, a book move of type `Reader::BookMove` called `book_move` can be used as follows:
- `book_move.toFile` returns the index of the file of the target square 
- `book_move.toRow` returns the index of the row of the target square
- `book_move.fromFile` returns the index of the file of the source square
- `book_move.fromRow` returns the index of the row of the source square
- `book_move.promotion` returns the type of the promoted piece

**FILES**: a is 0, b is 1, ... h is 7

**ROWS**: 0, 1, ... 7

**PROMOTIONS**: 0 is none, 1 is knight, 2 is bishop, 3 is rook, 4 is queen

Or you can just call `Reader::ConvertBookMoveToUci(book_move)` and automatically convert a move to the UCI format

## :abc: Code example
```
Reader::Book book;
book.Load("book.bin");
chess::Board board = chess::Board();
board.makeMove("e2e4");
board.makeMove("e7e5");
Reader::BookMoves book_moves = book.GetBookMoves((uint64_t)board.zobrist());
std::cout << Reader::ConvertBookMoveToUci(Reader::RandomBookMove(book_moves)) << std::endl;
book.Clear();
```
**OUTPUT:** `g1f3`

## :computer: How to help?
Please suggest improvements to the library.
I have done my best to eradicate all _known_ bugs from the code. However, if you feel you have found a potential bug, please open a pull request.
