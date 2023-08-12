# Typing Indicator
Add typing indicator logic to your JavaScript chat app. Typing-indicator is framework agnostic and works with any JavaScript frameworks (or without).

## Example
### JavaScript
```javascript
import TypingIndicator from 'typing-indicator';
const typingIndicator = new TypingIndicator();
typingIndicator.listen(isTyping => {
  console.log('Is typing?', isTyping);
});
HTMLInputElementObject.addEventListener('input', e => {
  typingIndicator.onChange(e.value);
});
```


### React
```javascript
import TypingIndicator from 'typing-indicator';

class Input extends Component {
  state = {
    text: "",
    typingIndicator: new TypingIndicator(),
  }

  componentDidMount() {
    const {typingIndicator} = this.state;
    const {onChangeTypingState} = this.props;
    typingIndicator.listen(isTyping => onChangeTypingState(isTyping));
  }

  onChange(e) {
    const {typingIndicator} = this.state;
    const text = e.target.value;
    typingIndicator.onChange(text);
    this.setState({text});
  }

  onSubmit(e) {
    const {onSendMessage} = this.props;
    const {text} = this.state;
    e.preventDefault();
    this.setState({text: ""});
    onSendMessage(text);
  }

  render() {
    return (
      <div className="Input">
        <form onSubmit={e => this.onSubmit(e)}>
          <input
            onChange={e => this.onChange(e)}
            value={this.state.text}
            type="text"
            placeholder="Enter your message and press ENTER"
            autoFocus
          />
          <button>Send</button>
        </form>
      </div>
    );
  }
}

export default Input;
```