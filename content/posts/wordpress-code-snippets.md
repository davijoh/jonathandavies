+++
date = 2022-08-29T12:00:00Z
draft = true
showToc = true
tags = ["Wordpress", "Code Snippets"]
title = " 🙌 Useful Code Snippets for Wordpress"

+++
# My list of useful code snippets for WordPress

Most of the websites I work on are built using WordPress (Gutenberg) and Elementor.

Now, this combination isn't perfect and there are some -very frustrating- limitations to the existing functionalities.

For example, how come Gutenberg blocks don't include a table of contents block? Do I really have to install a plugin or add one manually to each post?!

Or what do I do if I want to block non-professional email domains on my Elementor forms? Another plugin, really?!

This rapidly adds up, especially since a few lines of code can easily replace many plugins. Plus, I personally try to keep my plugins count to a minimum because they make the website heavier and can be the source of compatibility issues or hacks.

Unfortunately, my coding skills are very limited, but many website owners/builders are in the same situation and there are always friendly developers to help us out.

Here is some handy code that I've found over time.

## Blacklist/block email domains on Elementor forms

This is particularly useful in 2 situations:

1. You want to allow professional email addresses only and block generic domains such as Gmail, Hotmail or Yahoo.
2. You keep getting spam from the same email domain

Note: To add, or remove a domain to the backlist, edit the list under "$black_list_domains = \["

    // Blacklist email domains for element or forms
    
    add_action( 'elementor_pro/forms/validation/email', function( $field, $record, $ajax_handler ) {
    	// validate email format
    	if ( ! is_email( $field['value'] ) ) {
    		$ajax_handler->add_error( $field['id'], 'Invalid Email address, it must be in the format XX@XX.XX' );
    		return;
    	}
    
    	$black_list_domains = [
    		'gmail.com',
    		'yahoo.com',
    		'hotmail.com',
    		'outlook.com',
    		'hotmail.fr',
    	];
    
    	$email_domain = explode( '@', $field['value'] )[1];
    
    	if ( in_array( $email_domain, $black_list_domains ) ) {
    		$ajax_handler->add_error( $field['id'], 'Please enter a Business Email address, emails from the domain ' . $email_domain . ' are not allowed.' );
    		return;
    	}
    }, 10, 3 );

[Source](https://brandforward.nl/uncategorized/spam-deels-voorkomen-met-een-email-blacklist-in-elementor/ "source")

## Add a contact to a Mailchimp audience only if opt-in (Elementor forms)

Elementor forms are great and they integrate easily with email marketing tools such as Mailchimp and GetResponse.

One of the features they offer is to automatically add a contact to an audience (from your email marketing tool) after the contact fills out a form.

But there is no simple way to add the contact only if he ticks an acceptance field (checkbox).

The following code snippet fixes that.

Note: For the snippet to work, you need to add an id (in Elementor) that starts with "mailchimp_accept" for the checkbox. Eg: "mailchimp_accept_popup" or "mailchimp_accept_contact_page".

    // Mailchimp opt-in checkbox for Elementor Form
    // Version 2.0 - This one also works when you use Mailchimp tags
    add_filter('pre_http_request', function($preempt, $parsed_args, $url) {
        // Only run this code when an Elementor Pro form has been submitted
        if (!isset($_POST['action']) || $_POST['action'] != 'elementor_pro_forms_send_form') {
            return $preempt;
        }
    
        // Only run this when trying to contact the Mailchimp API
        if (strpos($url, 'api.mailchimp.com') !== false) {
            $form_fields = $_POST['form_fields'] ?? [];
    
            if (!is_array($form_fields) || empty($form_fields)) {
                return $preempt;
            }
            
            // Check if there is an opt-in field defined that start with mailchimp_accept
            $ID = "";
            foreach(array_keys($form_fields) as $formKey)
            {
                if(strpos($formKey, "mailchimp_accept") !== false)
                    $ID = $formKey;
            }
    
            // If not found any key means not approved
            if (empty($ID)) {
                // Short-circuit Mailchimp API call
                return [
                    'headers' => '',
                    'body' => '{"simulation":true}',
                    'response' => [
                        'code' => substr($url, -5) === '/tags' ? 204 : 200,
                        'message' => 'OK',
                    ],
                    'cookies' => '',
                    'filename' => '',
                ];
            }
        }
    
        return $preempt;
    }, PHP_INT_MAX, 3);

[Source](https://github.com/elementor/elementor/issues/10038 "Source")

## Add an automatic table of contents in articles using a shortcode block

I never understood why Gutenberg doesn't include a TOC block in their reusable blocks.

Of course, table of contents can be added manually but this isn't convenient when we simply need an automatic table of contents generated from the article headings.

The following snippet lets you add an automatic TOC, simply by adding a shortcode block (Gutenberg) into your article, where you want the TOC to appear, and write "\[TOC\]" into the block.

    // Automatic TOC
    
    function get_toc($content) {
      // get headlines
      $headings = get_headings($content);
    
      // parse toc
      ob_start();
      echo "<div class='table-of-contents'>";
      echo "<span class='toc-headline'>Sommaire</span>";
      parse_toc($headings, 0, 0);
      echo "</div>";
      return ob_get_clean();
    }
    
    function parse_toc($headings, $index, $recursive_counter) {
      // prevent errors
      if($recursive_counter > 60 || !count($headings)) return;
    
      // get all needed elements
      $last_element = $index > 0 ? $headings[$index - 1] : NULL;
      $current_element = $headings[$index];
      $next_element = NULL;
      if($index < count($headings) && isset($headings[$index + 1])) {
        $next_element = $headings[$index + 1];
      }
    
      // end recursive calls
      if($current_element == NULL) return;
    
    
      // get all needed variables
      $tag = intval($headings[$index]["tag"]);
      $id = $headings[$index]["id"];
      $classes = isset($headings[$index]["classes"]) ? $headings[$index]["classes"] : array();
      $name = $headings[$index]["name"];
    
    
      // element not in toc
      if(isset($current_element["classes"]) && $current_element["classes"] && in_array("nitoc", $current_element["classes"])) {
        parse_toc($headings, $index + 1, $recursive_counter + 1);
        return;
      }
    
    
      // parse toc begin or toc subpart begin
      if($last_element == NULL || $last_element["tag"] < $tag) echo "<ul>";
    
    
      // build li class
      $li_classes = "";
      if(isset($current_element["classes"]) && $current_element["classes"] && in_array("toc-bold", $current_element["classes"])) $li_classes = " class='bold'";
    
      // parse line begin
      echo "<li" . $li_classes .">";
    
      // only parse name, when li is not bold
      if(isset($current_element["classes"]) && $current_element["classes"] && in_array("toc-bold", $current_element["classes"])) {
        echo $name;
      } else {
        echo "<a href='#" . $id . "'>" . $name . "</a>";
      }
    
      if($next_element && intval($next_element["tag"]) > $tag) {
        parse_toc($headings, $index + 1, $recursive_counter + 1);
      }
    
      // parse line end
      echo "</li>";
    
      // parse next line
      if($next_element && intval($next_element["tag"]) == $tag) {
        parse_toc($headings, $index + 1, $recursive_counter + 1);
      }
    
    
      // parse toc end or toc subpart end
      if ($next_element == NULL || ($next_element && $next_element["tag"] < $tag)) {
        echo "</ul>";
    
        if ($next_element && $tag - intval($next_element["tag"]) >= 2) {
          echo "</li></ul>";
        }
      }
    
      // parse top subpart
      if($next_element != NULL && $next_element["tag"] < $tag) {
        parse_toc($headings, $index + 1, $recursive_counter + 1);
      }
    }
    
    function get_headings($content) {
      $headings = array();
      preg_match_all("/<h([1-2])(.*)>(.*)<\/h[1-2]>/", $content, $matches);
      
      for($i = 0; $i < count($matches[1]); $i++) {
    
        $headings[$i]["tag"] = $matches[1][$i];
    
        // get id
        $att_string = $matches[2][$i];
        preg_match("/id=\"([^\"]*)\"/", $att_string , $id_matches);
        $headings[$i]["id"] = $id_matches[1];
    
        // get classes
        $att_string = $matches[2][$i];
        preg_match_all("/class=\"([^\"]*)\"/", $att_string , $class_matches);
        for($j = 0; $j < count($class_matches[1]); $j++) {
          $headings[$i]["classes"][] = $class_matches[1][$j];
        }
    
        $headings[$i]["name"] = $matches[3][$i];
      }
    
      return $headings;
    }
    
    function toc_shortcode() {
        return get_toc(auto_id_headings(get_the_content()));
    }
    add_shortcode('TOC', 'toc_shortcode');
    
    /**
     * Automatically add IDs to headings such as <h2></h2>
     */
    function auto_id_headings( $content ) {
      $content = preg_replace_callback('/(\<h[1-6](.*?))\>(.*)(<\/h[1-6]>)/i', function( $matches ) {
        if(!stripos($matches[0], 'id=')) {
          $matches[0] = $matches[1] . $matches[2] . ' id="' . sanitize_title( $matches[3] ) . '">' . $matches[3] . $matches[4];
        }
        return $matches[0];
      }, $content);
        return $content;
    }
    add_filter('the_content', 'auto_id_headings');

[Source](https://webdeasy.de/en/wordpress-table-of-contents-without-plugin/  "Source")  
  
Note: The following code only includes h2 headings in the TOC. If you want to include other headings (h3 and h4 for example) you need to edit the code. To do so, look for this section in the code:

    function get_headings($content) {
      $headings = array();
      preg_match_all("/<h([1-2])([^<]*)>(.*)<\/h[1-2]>/", $content, $matches);

In the third line, replace "1-2" with the values corresponding to the range of headings you want to include. Eg. Replace "1-2" with "1-4" to include headings up to h4.