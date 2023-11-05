**Ex**: Tokenizer class
```
public class Tokenizer{
    public static final SymbolPair[] SYMBOLS = new SymbolPair[]{
        new SymbolPair("(", new LeftParenToken())
        new SymbolPair(")", new RightParenToken())
        new SymbolPair("=", new SingleEqualsToken())
        new SymbolPair("+", new PlusToken())
        *etc.*
    }
}
 ```    
    - Organizing it like this not only makes it readable but helps save memory as well

**Ex**: Tokenizer function: reading in identifiers or reserved words
```
public Token tokenizeIdentifierOrReservedWord(){
    String name = "";
    if(Character.isLetter(input.charAt(position))){
        name += input.charAt(position);
        position++;
        while(Character.isLetterOrDigit(input.charAt(position))){
            name += input.charAt(position);
            position++;
        }
        if (name.equals("int")){
            return new IntToken();
        }
        else if (name.equals("bool")){
            return new BoolToken();
        }
        else if (name.equals("vardec")){
            return new VardecToken();
        }
        *etc.*
        else {
            return new IdentifierToken(name);
        } 
    }
    else {return null};
}
```
*Same process for tokenizing symbols (", +, =)*
- Able to read token -> add to array list of tokens
- Unable to read token -> probably hit something we don't recognize, or ran out of characters. Presents a problem