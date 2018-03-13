# mobile-toggle-dropdowns
Giving dropdowns to mobile menus with arrows

Adding Arrow Span Drop Downs to Mobile Menus
1.  Add This to the JS file

/* Drop Down Navigation */
var menuContainer = '#navigation ';
// var thisLink;
( function( $ ) {
$( document ).ready(function() {
	$(menuContainer + '>div>ul>li.menu-item-has-children').append('<span class="holder"></span>');
	$(menuContainer + 'li.menu-item-has-children>span.holder').on('click', function(){
			var element = $(this).parent('li');
			if (element.hasClass('open')) {
				element.removeClass('open');
				element.find('li').removeClass('open');
				element.find('ul').slideUp();
				// $(this).attr('href', thisLink);
			}
			else {
				// thisLink = this.getAttribute('href');
				element.addClass('open');
				element.children('ul').slideDown();
				element.siblings('li').children('ul').slideUp();
				element.siblings('li').removeClass('open');
				element.siblings('li').find('li').removeClass('open');
				element.siblings('li').find('ul').slideUp();
				// $(this).removeAttr('href');
			}
		});
	(function getColor() {
		var r, g, b;
		var textColor = $(menuContainer).css('color');
		textColor = textColor.slice(4);
		r = textColor.slice(0, textColor.indexOf(','));
		textColor = textColor.slice(textColor.indexOf(' ') + 1);
		g = textColor.slice(0, textColor.indexOf(','));
		textColor = textColor.slice(textColor.indexOf(' ') + 1);
		b = textColor.slice(0, textColor.indexOf(')'));
		var l = rgbToHsl(r, g, b);
		if (l > 0.7) {
			$(menuContainer + '>ul>li>a').css('text-shadow', '0 1px 1px rgba(0, 0, 0, .35)');
			$(menuContainer + '>ul>li>span').css('border-color', 'rgba(0, 0, 0, .35)');
		}
		else
		{
			$(menuContainer +  '>ul>li>a').css('text-shadow', '0 1px 0 rgba(255, 255, 255, .35)');
			$(menuContainer +  '>ul>li>span').css('border-color', 'rgba(255, 255, 255, .35)');
		}
	})();

	function rgbToHsl(r, g, b) {
	    r /= 255, g /= 255, b /= 255;
	    var max = Math.max(r, g, b), min = Math.min(r, g, b);
	    var h, s, l = (max + min) / 2;

	    if(max == min){
	        h = s = 0;
	    }
	    else {
	        var d = max - min;
	        s = l > 0.5 ? d / (2 - max - min) : d / (max + min);
	        switch(max){
	            case r: h = (g - b) / d + (g < b ? 6 : 0); break;
	            case g: h = (b - r) / d + 2; break;
	            case b: h = (r - g) / d + 4; break;
	        }
	        h /= 6;
	    }
	    return l;
	}
});
} )( jQuery );


2.  Add these Styles to the Styles.css file or wherever your dropdowns and menu LI items may live
/* Adding Arrow Click Dropdowns To Mobile Menu */
.holder{
    display: none;
}

@media (max-width: 991px) {
      .menu-main-navigation-container>ul{
        -webkit-box-orient: vertical;-webkit-box-direction: normal;-ms-flex-direction: column;flex-direction: column;
      }
      .menu-main-navigation-container{
        background-color: #393be5;
      }
    #navigation ul li a{
        padding:10px 30px 10px 0px;
        text-align: right;
    }
    #navigation ul li{
        width:100%;
        text-align: right;
    }
    #navigation ul li ul{
        width: 100%;
        position: relative;
        padding-top: 0px;
        margin-top: 0px;
    }
    #navigation ul li:hover ul{
        position: relative;
        display: none;
    }
    #navigation ul ul li a{
        width: 100% !important;
    }
    #navigation ul li:hover a{
        width: 100%;
    }
    .menu li.has-children > a:after{
        display: none;
    }
    #navigation ul ul li:hover ul, #navigation ul li:hover ul li:hover ul{
        display: none;
    }
    /* Drop Down Arrows  Mobile */
/* Drop Down Arrows */
#navigation > ul > li > a:hover,
#navigation > ul > li.active > a,
#navigation > ul > li.open > a {
  color: #eeeeee;
  background: #1fa0e4;
  background: -webkit-linear-gradient(#1fa0e4, #1992d1);
  background: -moz-linear-gradient(#1fa0e4, #1992d1);
  background: -o-linear-gradient(#1fa0e4, #1992d1);
  background: -ms-linear-gradient(#1fa0e4, #1992d1);
  background: linear-gradient(#1fa0e4, #1992d1);
}

#navigation > ul > li.open > a {
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.15), 0 1px 1px rgba(0, 0, 0, 0.15);
  border-bottom: 1px solid #1682ba;
}
li.open .holder {
  transform: rotate(0);
}
.holder {
  display: block;
  position: absolute;
  top: 4px;
  right: 0px;
  z-index: 1000;
  width: 30px;
  height: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #ffffff;
  transform: rotate(180deg);
  transition: all 350ms ease;
}
/*.holder:hover{
  background: #1b1b1b80;
}*/
.holder::before {
  display: inline-block;
  content: "";
  width: 6px;
  height: 6px;
  right: 20px;
  z-index: 10;
  -webkit-transform: rotate(-135deg);
  -moz-transform: rotate(-135deg);
  -ms-transform: rotate(-135deg);
  -o-transform: rotate(-135deg);
  transform: rotate(-135deg);
  color: #ffffff;
}
.holder::after {
  top: 17px;
  border-top: 2px solid #ffffff;
  border-left: 2px solid #ffffff;
}
#navigation > ul > li > a:hover > span::after,
#navigation > ul > li.active > a > span::after,
#navigation > ul > li.open > a > span::after {
  border-color: #eeeeee;
}
.holder::before {
  top: 18px;
  border-top: 2px solid;
  border-left: 2px solid;
  border-top-color: inherit;
  border-left-color: inherit;
}
#navigation > ul > li > a:hover > span::after,
#navigation > ul > li.active > a > span::after,
#navigation > ul > li.open > a > span::after {
  border-color: #eeeeee;
}
#navigation ul ul li:hover > a,
#navigation ul ul li.open > a,
#navigation ul ul li.active > a {
  background: #424852;
  color: #ffffff;
}
#navigation > ul > li > ul > li.open:last-child > a,
#navigation > ul > li > ul > li.last.open > a {
  border-bottom: 1px solid #32373e;
}
#navigation > ul > li > ul > li.open:last-child > ul > li:last-child > a {
  border-bottom: 0;
}
#navigation ul ul li.active > a::after,
#navigation ul ul li.open > a::after,
#navigation ul ul li > a:hover::after {
  border-color: #ffffff;
  }
}
