## Bash Definitions and Reserved Words

### Bash Definitions

<table>
  <tr>
    <td><b>blank</b></td><td>A space or tab.</td>
  </tr>
  <tr>
    <td><b>word</b></td><td>A sequence of characters considered as a single unit by the shell. Also know as a <b>token</b>.</td>
  </tr>
  <tr>
  <td><b>name</b></td><td>A <em>word</em> consisting only of alphanumeric characters and underscores, and beginning with an alphabetic character or an underscore. Also referred to as an <b>identifier</b>.</td>
  </tr>
  <tr>
  <td><b>metacharacter</b></td><td>A character that, when unquoted, separates <em>words</em>. One of the following:<br><br><b>&#124;</b> <b>&#38;</b> <b>&#59;</b> <b>&#40;</b> <b>&#41;</b> <b>&#60;</b> <b>&#62;</b> <b>space</b> <b>tab</b></td>
  </tr>
  <tr>
  <td><b>control operator</b></td><td>A <em>token</em> that performs a control function. It is one of the following symbols:<br><br><b>&#63732;&#63732;</b> <b>&#38;</b> <b>&#38;&#38;</b> <b>&#59;</b> <b>&#59;&#59;</b> <b>&#40;</b> <b>&#41;</b> <b>&#124;</b> <b>&#60;newline&#62;</b></td>
  </tr>
</table>

---
### Bash Reserved Words

_Reserved words_ are words that have a special meaning to the shell. The following words are recognized as reserved when unquoted and either the first word of a simple command or the third word of a **case** or **for** command:

- **!**
- **case**
- **do**
- **done**
- **elif**
- **else**
- **esac**
- **fi**
- **for**
- **function**
- **if**
- **in**
- **select**
- **then**
- **until**
- **while**
- **{**
- **}**
- **time**
- **[[**
- **]]**
