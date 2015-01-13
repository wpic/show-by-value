Simple jquery plugin to show and hide inputs in the form by value of the other inputs in the form.


```javascript
(function ( $ ) {

    $.fn.showByValue = function( options ) {

        return this.each(function(e) {
            var form = $(this);

            var apply_shows = function() {
                $('[data-show-by-value]', form).each(function() {
                    var list = $(this).attr('data-show-by-value').split(',');
                    for (l in list) {
                        var parts = list[l].split('=');

                        var selector = "[name='" + parts[0] + "']";
                        if (parts.length > 1) {
                            if ($(selector, form).val() === parts[1]) {
                                $(this).show();
                                return;
                            }
                        }
                        else if ($(selector, form).val()) {
                            $(this).show();
                            return;
                        }
                    }

                    $(this).hide();
                });
            }

            // handle shows
            $('select[name], input[name], textarea[name]', form).change(apply_shows);
            apply_shows();
        });
    }

} ( jQuery ));
```

# Sample


```html
<form>
    <select name="mode">
        <option>None</option>
        <option value="first">First</option>
        <option value="secound">Second</option>
    </select>
    <input data-show-by-value="mode=first" value="This is the first one" />
    <input data-show-by-value="mode=secound" value="This is the second one" />
    <input data-show-by-value="mode=first,mode=secound" value="One or two" />

    <br/>
    <input name="typing" type="text" value="clear to hide other one" />
    <input data-show-by-value="typing=" type="text" value="it's empty" />
    <input data-show-by-value="typing" type="text" value="it's not empty" />
</form>

<script>
$('form').showByValue();
</script>
```