# Framework by ReidenXerx

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

## Documentation
html {
	    font-family: 'Montserrat', sans-serif;
}

@include RadioCheck(nipple, 20, 5, 10,
$MAP-optional: (
"shadow-box": "inset 0px 2px 2px rgba(0, 0, 0, .3)",
"color": rgba(0, 359, 128, 1),
"background-color": (rgba(0, 259, 328, 1) #666),
"symbol": "\2714",
));

.main_screen {
	@include SetBackground(solid, rgba(42, 42, 46, 1));

	.main_container-vertical {
		@include SetWidth-responsive(1580);

		.main_title {
			@include SetFlexJustify(space-between);
			@include SetFlexAlign(center);
			@include SetPaddings(vertical, 330, 300, 0.8);

			.main_logo {
				@include SetWidth-responsive(715);
			}

			h1 {
				@include SetFontLineSize(0.3, 0.63, 0.07, 48, 14);
				@include SetFontVars(bold, 0.1, white, uppercase);

				.blue {
					@include SetFontLineSize(0.1, 0.8, 0.1, 84, 14);
					@include SetFontVars(bold, 0.1, rgba(0, 159, 228, 1), uppercase);
				}
			}

		@include _tablet-small {
			@include ToVertical();
			@include SetFlexJustify(space-between);
			@include SetFlexAlign(center);
			@include SetTextAlign(center);
		}

		}

	}
}
.main_container-grid {

	@include SetWidth-responsive(1580);
	@include SmartGrid(1500,

		$LIST-rows: ("first": 120, "five": 320) ("first": 350, "second": 611, "third": 345) ("four": 345)
	);

	.first {
		grid-area: first;
	}

	.second {
		grid-area: second;
	}

	.third {
		grid-area: third;
	}

	.four {
		grid-area: four;
	}

	.five {
		grid-area: five;
	}
}
 

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
