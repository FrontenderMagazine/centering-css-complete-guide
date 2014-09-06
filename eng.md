# Centering in CSS: A Complete Guide

Centering things in CSS is the poster child of CSS complaining. *Why does it have to be so hard?* They jeer. I think the issue isn't that it's difficult to do, but in that there so many different ways of doing it, depending on the situation, it's hard to know which to reach for.

So let's make it a decision tree and hopefully make it easier.

I need to center...

## Horizontally

### Is it inline or inline-* elements (like text or links)?

You can center inline elements horizontally, within a block-level parent element, with just:

    .center-children {
      text-align: center;
    }

<iframe id="cp_embed_HulzB" src="//codepen.io/chriscoyier/embed/HulzB?default-tab=result&amp;slug-hash=HulzB&amp;theme-id=1&amp;height=184&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="184" frameborder="0"></iframe>

This will work for inline, inline-block, inline-table, inline-flex, etc.

### Is it a block level element?

You can center a block-level element by giving it `margin-left` and `margin-right` of `auto` (and it has a set `width`, otherwise it would be full width and wouldn't need centering). That's often done with shorthand like this:

    .center-me {
      margin: 0 auto;
    }

<iframe id="cp_embed_eszon" src="//codepen.io/chriscoyier/embed/eszon?default-tab=result&amp;slug-hash=eszon&amp;theme-id=1&amp;height=200&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="200" frameborder="0"></iframe>

This will work no matter what the width of the block level element you're centering, or the parent.

Note that you can't `float` an element to the center. [There is a trick though.][1]

### Is there more than one block level element?

If you have two or more block-level elements that need to be centered horizontally *in a row*, chances are you'd be better served making them a different `display` type. Here's an example of making them `inline-block` and an example of flexbox:

<iframe id="cp_embed_ebing" src="//codepen.io/chriscoyier/embed/ebing?default-tab=result&amp;slug-hash=ebing&amp;theme-id=1&amp;height=438&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="438" frameborder="0"></iframe>

Unless you mean you have multiple block level elements stacked on top of each other, in which case the auto margin technique is still fine:

<iframe id="cp_embed_haCGt" src="//codepen.io/chriscoyier/embed/haCGt?default-tab=result&amp;slug-hash=haCGt&amp;theme-id=1&amp;height=352&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="352" frameborder="0"></iframe>

## Vertically

Vertical centering is a bit trickier in CSS.

### Is it inline or inline-* elements (like text or links)?

#### Is it a single line?

Sometimes inline / text elements can appear vertically centered, just because there is equal padding above and below them.

    .link {
      padding-top: 30px;
      padding-bottom: 30px;
    }

<iframe id="cp_embed_ldcwq" src="//codepen.io/chriscoyier/embed/ldcwq?default-tab=result&amp;slug-hash=ldcwq&amp;theme-id=1&amp;height=180&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="180" frameborder="0"></iframe>

If padding isn't an option for some reason, and you're trying to center some text that you know will not wrap, there is a trick were making the `line-height` equal to the height will `center` the text.

    .center-text-trick {
      height: 100px;
      line-height: 100px;
      white-space: nowrap;
    }

<iframe id="cp_embed_LxHmK" src="//codepen.io/chriscoyier/embed/LxHmK?default-tab=result&amp;slug-hash=LxHmK&amp;theme-id=1&amp;height=305&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="305" frameborder="0"></iframe>

#### Is it multiple lines?

Equal padding on top and bottom can give the centered effect for multiple lines of text too, but if that isn't going to work, perhaps the element the text is in can be a table cell, either literally or made to behave like one with CSS. The [`vertical-align`][2] property handles this, in this case, unlike what it normally does which is handle the alignment of elements aligned on a row. ([More on that.][3])

<iframe id="cp_embed_ekoFx" src="//codepen.io/chriscoyier/embed/ekoFx?default-tab=result&amp;slug-hash=ekoFx&amp;theme-id=1&amp;height=426&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="426" frameborder="0"></iframe>

If something table-like is out, perhaps you could use flexbox? A single flex-child can be made to center in a flex-parent pretty easily.

    .flex-center-vertically {
      display: flex;
      justify-content: center;
      flex-direction: column;
      height: 400px;
    }

<iframe id="cp_embed_uHygv" src="//codepen.io/chriscoyier/embed/uHygv?default-tab=result&amp;slug-hash=uHygv&amp;theme-id=1&amp;height=380&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="380" frameborder="0"></iframe>

Remember that it's only really relevant if the parent container has a fixed height (px, %, etc), which is why the container here has a height.

If both of these techniques are out, you could employ the "ghost element" technique, in which a full-height pseudo element is placed inside the container and the text is vertically aligned with that.

    .ghost-center {
      position: relative;
    }
    .ghost-center::before {
      content: " ";
      display: inline-block;
      height: 100%;
      width: 1%;
      vertical-align: middle;
    }
    .ghost-center p {
      display: inline-block;
      vertical-align: middle;
    }

<iframe id="cp_embed_ofwgD" src="//codepen.io/chriscoyier/embed/ofwgD?default-tab=result&amp;slug-hash=ofwgD&amp;theme-id=1&amp;height=392&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="392" frameborder="0"></iframe>

### Is it a block-level element?

#### Do you know the height of the element?

It's fairly common to *not* know the height in web page layout, for lots of reasons: if the width changes, text reflow can change the height. Variance in the styling of text can change the height. Variance in the amount of text can change the height. Elements with a fixed aspect ratio, like images, can change height when resized. Etc.

But if you do know the height, you can center vertically like:

    .parent {
      position: relative;
    }
    .child {
      position: absolute;
      top: 50%;
      height: 100px;
      margin-top: -50px; /* account for padding and border if not using box-sizing: border-box; */
    }

<iframe id="cp_embed_HiydJ" src="//codepen.io/chriscoyier/embed/HiydJ?default-tab=result&amp;slug-hash=HiydJ&amp;theme-id=1&amp;height=457&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="457" frameborder="0"></iframe>

#### Is the element of unknown height?

It's still possible to center it by nudging it up half of it's height after bumping it down halfway:

    .parent {
      position: relative;
    }
    .child {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
    }

<iframe id="cp_embed_lpema" src="//codepen.io/chriscoyier/embed/lpema?default-tab=result&amp;slug-hash=lpema&amp;theme-id=1&amp;height=469&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="469" frameborder="0"></iframe>

#### Can you use flexbox?

No big surprise, this is a lot easier in [flexbox][4].

    .parent {
      display: flex;
      flex-direction: column;
      justify-content: center;
    }

<iframe id="cp_embed_FqDyi" src="//codepen.io/chriscoyier/embed/FqDyi?default-tab=result&amp;slug-hash=FqDyi&amp;theme-id=1&amp;height=471&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="471" frameborder="0"></iframe>

## Both Horizontally and Vertically

You can combine the techniques above in any fashion to get perfectly centered elements. But I find this generally falls into three camps:

### Is the element of fixed width and height?

Using negative margins equal to half of that width and height, after you've absolutely positioned it at 50% / 50% will center it with great cross browser support:

    .parent {
      position: relative;
    }

    .child {
      width: 300px;
      height: 100px;
      padding: 20px;

      position: absolute;
      top: 50%;
      left: 50%;

      margin: -70px 0 0 -170px;
    }

<iframe id="cp_embed_JGofm" src="//codepen.io/chriscoyier/embed/JGofm?default-tab=result&amp;slug-hash=JGofm&amp;theme-id=1&amp;height=386&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="386" frameborder="0"></iframe>

### Is the element of unknown width and height?

If you don't know the width or height, you can use the transform property and a negative translate of 50% in both directions (it is based on the current width/height of the element) to center:

    .parent {
      position: relative;
    }
    .child {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }

<iframe id="cp_embed_lgFiq" src="//codepen.io/chriscoyier/embed/lgFiq?default-tab=result&amp;slug-hash=lgFiq&amp;theme-id=1&amp;height=412&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="412" frameborder="0"></iframe>

### Can you use flexbox?

To center in both directions with flexbox, you need to use two centering properties:

    .parent {
      display: flex;
      justify-content: center;
      align-items: center;
    }

<iframe id="cp_embed_msItD" src="//codepen.io/chriscoyier/embed/msItD?default-tab=result&amp;slug-hash=msItD&amp;theme-id=1&amp;height=404&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="404" frameborder="0"></iframe>

## Conclusion

You can totally center things in CSS.

[1]: http://css-tricks.com/float-center/
[2]: http://css-tricks.com/almanac/properties/v/vertical-align/
[3]: http://css-tricks.com/what-is-vertical-align/
[4]: http://css-tricks.com/snippets/css/a-guide-to-flexbox/