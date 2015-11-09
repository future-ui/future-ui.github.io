# Atomic Design

Atomic Design makes a loose analogy between chemistry and
interfaces. As such, the stages are defined in order of increasing
complexity: Atoms, Molecules, Organisms, Templates and Pages.

## Atoms

Atoms are the basic building blocks of UI. They have distinct
properties and can't be broken down further without losing their
meaning. For interfaces, atoms are basic tags, such as form labels,
inputs or buttons. They also include more abstract elements like color
palettes, fonts, and animations.

## Molecules

Molecules are groups of Atoms bonded together, which take on new
properties as a result. For example, a form label, search input, and
button atom can combine them together to form a search form molecule.
Building up from atoms to molecules encourages a “do one thing and do
it well” mentality, and encourages creating reusable interface
patterns.

## Organisms

Organisms are groups of molecules (and possibly atoms) joined together
to form distinct section of an interface. Organisms can consist of
similar and/or disparate molecule types. For example, a masthead
organism might consist of a logo, navigation, and search form, while a
“product grid” organism might consist of the same product info
molecule repeated over and over. Building up from molecules to
organisms encourages creating standalone, portable, reusable
components.

## Templates

With templates, we break our chemistry analogy. Templates are
comprised mostly of organisms combined together to form complete
views. Templates provide context for these relatively abstract
molecules and organisms, which is helpful for designers and clients
alike. Templates mostly focus on content structure (such as character
length, image size, etc) rather than the actual content.

## Pages

Pages are specific instances of templates. Pages are essential for
testing the effectiveness of the design system. This final form allows
us to loop back to modify our molecules, organisms, and templates to
better address the real context of the design.

Pages also provide a place to test variations in templates, such as
testing an article containing a 40-character-length headline and other
article with a 340-character-length headline. What does it look like
when a user has one item in their shopping cart versus 10 items with a
discount code applied? These specific page instances test the
resiliency of the system, influencing how the underlying molecules,
organisms, and templates are constructed.