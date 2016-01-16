<h1 id="gtwo_shield_for_arduino_due_tinyg_2">GTwo Shield for Arduino DUE &amp; TinyG 2</h1>

<p><a href="https://github.com/synthetos/TinyG">TinyG</a> is a 6 axis motion control system designed by Synthetos for driving CNC, Laser cutters, ans so on. It have been designed to run on Atmel ATxmega192. It&#8217;s a complete system (hard + soft).</p>

<p>Some faeatures : </p>

<ul>
<li>6 axis motion (XYZABC axes)</li>
<li>jerk controlled motion for acceleration planning (3rd order motion planning)</li>
<li>status displays (&#8216;?&#8217; character)</li>
<li>XON/XOFF and RTS/CTS protocol over USB serial</li>
<li>RESTful interface using JSON</li>
</ul>

<p><a href="https://github.com/synthetos/g2">TinyG 2</a> is a TinyG ARM port, also developed by Synthetos, working on Atmel Arm Processors, like the one used on low cost Arduino DUE. That port can be configured for using GRBL shields (Arduino Uno form factor) but unfortunately, pinout is slightly differents, so there&#8217;s no way to have more than 3 motors running. No commands, no emergency stops, spindle or homing&#8230; </p>

<p>GTwo is a shield designed to allow easy use or the port of TinyG with all functionnalities. </p>

<p><img src="imgs/GTwoShieldComplete.png" alt="GTwo assembly" title=""></p>

<p>That shield can be used :</p>

<ul>
<li>Directly connected to a <a href="https://www.google.fr/search?q=tb6560+red&amp;num=20&amp;safe=off&amp;source=lnms&amp;tbm=isch&amp;sa=X&amp;ved=0ahUKEwinnOrSrarKAhXkpnIKHYe3DXwQ_AUIBygB&amp;biw=917&amp;bih=418">TB 6560 &#8220;Red&#8221;</a>, for a maximum of 4 axis (X,Y,Z,A) and 4 GPIO inputs (I.E. homing X,Y,Z and emergency stop)</li>
<li>Connected thru 6 X 6 pins connectors to discrete drivers like Leadshine, Gekko, etc., allowing up to 6 axis (X,Y,Z,A,B,C).</li>
</ul>

<p><img src="imgs/BoardEnvironnement2.png" alt="GTwo assembly" title=""></p>

<h4 id="caracteristics">Caracteristics</h4>

<ul>
<li>Mostly passive shield, with all connectors for connecting spindle, PWM Spindle, coolant, homing &amp; Limits, switch for program control, up to 6 axis stepper driver boards</li>
<li>Since DUE is not 5V tolerant, limits inputs are level translated to be used @5V</li>
<li>All other inouts ARE not, and should no be connected to anything else than a 0V. (program control)</li>
</ul>

<h4 id="connections">Connections</h4>

<h5 id="when_using_a_tb6560_power_board_">When using a TB6560 power board :</h5>

<ul>
<li>JP1 : For connectig to a TB6560 &#8220;Red&#8221; Stepper driver board. A cable must be made with a HE10-26F > DB25F emulating parallel port. If using JP1, don&#8217;t use M1>M6</li>
<li>JP2 : Limits configuration for TB6560. Must be left unequipped if using M1 > M6 connections.</li>
<li>JP4 : Relay config. Must be left unequipped if using M1 > M6 connections.</li>
</ul>

<h5 id="when_using_m1_m6_connections_to_discrete_drivers">When using M1 > M6 connections to discrete drivers</h5>

<ul>
<li>M1 > M6 : Allows to connect up to 6 steppers motors (X/Y/Z/A/B/C). If using M1>M6, don&#8217;t use JP1.</li>
<li>JP3 : Limits inputs. Allow to connect limit and/or homing switches (X-, X+, Y-, Y+, Z-, Z+), emergency stop and optionnaly Hardware interlock. All inputs are 5V tolerant.</li>
<li>JP6 : Stepper power conf </li>
</ul>

<p>M1 to M6 pinout :
* Broche 1 : Step
* Broche 2 : Dir
* Broche 3 : Enable motor (independant enable for each axis)
* Broche 4 : GND
* Broche 5 : Global Enable for all axis
* Broche 6 : VCC (3.3V or 5V depending of JP6) setting</p>

<h5 id="other_connectors_">Other connectors :</h5>

<ul>
<li>JP5 : Spindle &amp; Coolant outputs (3.3V). &#8220;Spindle&#8221; is for Spindle on/off, &#8220;dir&#8221; is for spindle direction (CW/CCW), &#8220;PWM&#8221; is for connecting a PWM spindle, &#8220;PW2&#8221; is an optionnal secondary PWM, &#8220;Cool&#8221; is for connecting cooolant command. </li>
<li>JP7 : Control inputs. Connect swtches for Soft Reset (SR), Feed Hold (Hold), Cycle Start (Run), Emergency Stop (ESTP) or hardware reset (RST)</li>
</ul>

<h5 id="configuration_jumpers_">Configuration Jumpers :</h5>

<p>JP2 : Must be equipped with 4 jumpers allowing to route X- or X+ to Pin 10 of parallel port, Y- or Y+ to pin 11 of parallel port, Z-or Z+ on pin 12 of paralel port, and emergency stop or hardware interlock on pin 13 of parallel port. 
JP4 : Must be equipped with 1 jumper allowing to route motor or coolant to the embedded relay of TB6560 red board.
JP6 : Must be equipped with 1 jumper to route a 3.3V or a 5V to M1 > M6 pin 6.</p>

<h5 id="associated_documents_">Associated Documents :</h5>

<ul>
<li><a href="GTwoShieldSchematics.pdf">Schematics</a></li>
<li><a href="partlist.txt">BOM</a></li>
<li><a href="GTwoShield.zip">ZIP archive for manufacturing</a></li>
<li><a href="imgs/DUE tinyG2 pinout 0.2.pdf">Due Pinout for Tiny G2</a></li>
<li><a href="imgs/GTwoShieldAssembly.pdf">Assembly</a></li>
<li><a href="imgs/GTwoShieldTop.png">Top view</a></li>
<li><a href="imgs/GTwoShieldBottom.png">Bottom view</a></li>
</ul>

<h5 id="example_configuration_">Example configuration :</h5>

<p>This configuration fits to a machine with origin switches at the bottom left ad top Z, for a CNC machine. GTtwo is connected to a TB6560 driver board, and board relay is used to power the spindle. (motor = M3/M5 Gcode). 
TB6560 inputs are Xmin, Ymin, ZMax, Emergency stop. A 3.3V is routed to M1>M6 pin 6.</p>

<p><img src="imgs/JumpersDefault.png" alt="GTwo Default Configuration" title=""></p>
