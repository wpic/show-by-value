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
                        if ($(selector, form).val() === parts[1]) {
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
</form>

<script>
$('form').showByValue();
</script>
```