<template>
  <v-app>
    <v-app-bar app color="pink accent-3" dark>
      <div class="d-flex align-center">
        <!-- <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        /> -->
      </div>

      <v-spacer></v-spacer>

      <v-btn href="https://fitpet.vercel.app" target="_blank" text>
        <span class="mr-2">FitPet</span>
        <!-- <v-icon>mdi-open-in-new</v-icon> -->
      </v-btn>
    </v-app-bar>

    <v-main>
      <v-app id="inspire">
        <v-card
          class="mx-auto mt-4"
          color="grey lighten-4"
          max-width="600"
          width="100%"
        >
          <v-card-title>
            <v-icon
              :color="checking ? 'red lighten-2' : 'pink accent-3'"
              class="mr-12"
              size="64"
              @click="takePulse"
            >
              mdi-dog
            </v-icon>
            <v-row align="start">
              <div class="text-caption grey--text text-uppercase">
                Random Dog Facts
              </div>
            </v-row>

            <v-spacer></v-spacer>

            <v-btn icon class="align-self-start" size="28" @click="randomGen">
              <v-icon>mdi-refresh</v-icon>
            </v-btn>
          </v-card-title>

          <v-card-text class="text-h5 font-weight-bold">
            {{ dogFacts[randomFact].fact }}
          </v-card-text>
        </v-card>

        <v-card
          class="mx-auto mt-4"
          color="grey lighten-4"
          max-width="600"
          width="100%"
        >
          <v-card-title>
            <v-icon
              :color="checking ? 'red lighten-2' : 'pink accent-3'"
              class="mr-12"
              size="64"
              @click="takePulse"
            >
              mdi-thermometer
            </v-icon>
            <v-row align="start">
              <div class="text-caption grey--text text-uppercase">
                Temperature
              </div>
              <div>
                <span
                  class="text-h3 font-weight-black"
                  v-text="Math.round((avg / 2.59) * 10) / 10 || '—'"
                ></span>
                <strong v-if="avg">⁰C</strong>
              </div>
            </v-row>

            <v-spacer></v-spacer>

            <v-btn icon class="align-self-start" size="28">
              <v-icon>mdi-arrow-right-thick</v-icon>
            </v-btn>
          </v-card-title>

          <v-sheet color="transparent">
            <v-sparkline
              :key="String(avg)"
              :smooth="16"
              :gradient="['#f72047', '#ffd200', '#1feaea']"
              :line-width="3"
              :value="heartbeats"
              auto-draw
              stroke-linecap="round"
            ></v-sparkline>
          </v-sheet>
        </v-card>

        <v-card
          class="mx-auto mt-2"
          color="grey lighten-4"
          max-width="600"
          width="100%"
        >
          <v-card-title>
            <v-icon
              :color="checking ? 'red lighten-2' : 'pink accent-3'"
              class="mr-12"
              size="64"
              @click="takePulse"
            >
              mdi-sleep
            </v-icon>
            <v-row align="start">
              <div class="text-caption grey--text text-uppercase">sleep</div>
              <div>
                <span
                  class="text-h3 font-weight-black"
                  v-text="Math.round((avg / 14.29) * 10) / 10 || '—'"
                ></span>
                <strong v-if="avg">Hrs</strong>
              </div>
            </v-row>

            <v-spacer></v-spacer>

            <v-btn icon class="align-self-start" size="28">
              <v-icon>mdi-arrow-right-thick</v-icon>
            </v-btn>
          </v-card-title>

          <v-sheet color="transparent">
            <v-sparkline
              :key="String(avg)"
              :smooth="16"
              :gradient="['#f72047', '#ffd200', '#1feaea']"
              :line-width="3"
              :value="heartbeats"
              auto-draw
              stroke-linecap="round"
            ></v-sparkline>
          </v-sheet>
        </v-card>

        <v-card
          class="mx-auto mt-2"
          color="grey lighten-4"
          max-width="600"
          width="100%"
        >
          <v-card-title>
            <v-icon
              :color="checking ? 'red lighten-2' : 'pink accent-3'"
              class="mr-12"
              size="64"
              @click="takePulse"
            >
              mdi-heart-pulse
            </v-icon>
            <v-row align="start">
              <div class="text-caption grey--text text-uppercase">Pulse</div>
              <div>
                <span
                  class="text-h3 font-weight-black"
                  v-text="avg || '—'"
                ></span>
                <strong v-if="avg">BPM</strong>
              </div>
            </v-row>

            <v-spacer></v-spacer>

            <v-btn icon class="align-self-start" size="28">
              <v-icon>mdi-arrow-right-thick</v-icon>
            </v-btn>
          </v-card-title>

          <v-sheet color="transparent">
            <v-sparkline
              :key="String(avg)"
              :smooth="16"
              :gradient="['#f72047', '#ffd200', '#1feaea']"
              :line-width="3"
              :value="heartbeats"
              auto-draw
              stroke-linecap="round"
            ></v-sparkline>
          </v-sheet>
        </v-card>

        <v-card
          class="mx-auto mt-2"
          color="grey lighten-4"
          max-width="600"
          width="100%"
        >
          <v-card-title>
            <v-icon
              :color="checking ? 'red lighten-2' : 'pink accent-3'"
              class="mr-12"
              size="64"
              @click="takePulse"
            >
              mdi-lungs
            </v-icon>
            <v-row align="start">
              <div class="text-caption grey--text text-uppercase">
                Breathing
              </div>
              <div>
                <span
                  class="text-h3 font-weight-black"
                  v-text="Math.round((avg / 66.67) * 10) / 10 || '—'"
                ></span>
                <strong v-if="avg">L</strong>
              </div>
            </v-row>

            <v-spacer></v-spacer>

            <v-btn icon class="align-self-start" size="28">
              <v-icon>mdi-arrow-right-thick</v-icon>
            </v-btn>
          </v-card-title>

          <v-sheet color="transparent">
            <v-sparkline
              :key="String(avg)"
              :smooth="16"
              :gradient="['#f72047', '#ffd200', '#1feaea']"
              :line-width="3"
              :value="heartbeats"
              auto-draw
              stroke-linecap="round"
            ></v-sparkline>
          </v-sheet>
        </v-card>
      </v-app>
    </v-main>
  </v-app>
</template>

<script>
const exhale = (ms) => new Promise((resolve) => setTimeout(resolve, ms));
export default {
  name: "App",
  data: () => ({
    checking: false,
    heartbeats: [],
    dogFacts: [
      {
        fact: "All dogs can be traced back 40 million years ago to a weasel-like animal called the Miacis which dwelled in trees and dens. The Miacis later evolved into the Tomarctus, a direct forbear of the genus Canis, which includes the wolf and jackal as well as the dog.",
      },
      {
        fact: "Ancient Egyptians revered their dogs. When a pet dog would die, the owners shaved off their eyebrows, smeared mud in their hair, and mourned aloud for days.",
      },
      {
        fact: "Small quantities of grapes and raisins can cause renal failure in dogs. Chocolate, macadamia nuts, cooked onions, or anything with caffeine can also be harmful.",
      },
      {
        fact: "Apple and pear seeds contain arsenic, which may be deadly to dogs.",
      },
      {
        fact: "Rock star Ozzy Osborne saved his wife Sharon’s Pomeranian from a coyote by tackling ad wresting the coyote until it released the dog.",
      },
      { fact: "Dogs have sweat glands in between their paws." },
      {
        fact: 'In 2003, Dr. Roger Mugford invented the "wagometer," a device that claims to interpret a dog’s exact mood by measuring the wag of its tail.',
      },
      {
        fact: 'Dogs have three eyelids. The third lid, called a nictitating membrane or "haw," keeps the eye lubricated and protected.',
      },
      {
        fact: "A dog’s shoulder blades are unattached to the rest of the skeleton to allow greater flexibility for running.",
      },
      {
        fact: "Puppies are sometimes rejected by their mother if they are born by cesarean and cleaned up before being given back to her.",
      },
      {
        fact: 'The phrase "raining cats and dogs" originated in seventeenth-century England. During heavy rainstorms, many homeless animals would drown and float down the streets, giving the appearance that it had actually rained cats and dogs.',
      },
      {
        fact: "During the Middle Ages, Great Danes and Mastiffs were sometimes suited with armor and spiked collars to enter a battle or to defend supply caravans.",
      },
      {
        fact: "Pekingese and Japanese Chins were so important in the ancient Far East that they had their own servants and were carried around trade routes as gifts for kings and emperors. Pekingese were even worshipped in the temples of China for centuries.",
      },
      {
        fact: "The shape of a dog’s face suggests how long it will live. Dogs with sharp, pointed faces that look more like wolves typically live longer. Dogs with very flat faces, such as bulldogs, often have shorter lives.",
      },
      {
        fact: "After the fall of Rome, human survival often became more important than breeding and training dogs. Legends of werewolves emerged during this time as abandoned dogs traveling in packs commonly roamed streets and terrified villagers.",
      },
      {
        fact: "During the Middle Ages, mixed breeds of peasants’ dogs were required to wear blocks around their necks to keep them from breeding with noble hunting dogs. Purebred dogs were very expensive and hunting became the province of the rich.",
      },
      {
        fact: "The most dogs ever owned by one person were 5,000 Mastiffs owned by Kublai Khan.",
      },
      {
        fact: "The American Kennel Club, the most influential dog club in the United States, was founded in 1884.",
      },
      {
        fact: "The most popular male dog names are Max and Jake. The most popular female dog names are Maggie and Molly.",
      },
      {
        fact: "Scholars have argued over the metaphysical interpretation of Dorothy’s pooch, Toto, in the Wizard of Oz. One theory postulates that Toto represents Anubis, the dog-headed Egyptian god of death, because Toto consistently keeps Dorothy from safely returning home.",
      },
      {
        fact: "Weird dog laws include allowing police offers in Palding, Ohio, to bite a dog to quiet it. In Ventura County, California, cats and dogs are not allowed to have sex without a permit.",
      },
      {
        fact: "The first dog chapel was established in 2001. It was built in St. Johnsbury, Vermont, by Stephan Huneck, a children’s book author whose five dogs helped him recuperate from a serious illness.",
      },
      {
        fact: "Those born under the sign of the dog in Chinese astrology are considered to be loyal and discreet, though slightly temperamental.",
      },
      {
        fact: "In Iran, it is against the law to own a dog as a pet. However, if an owner can prove the dog is a guard or hunting dog, this restriction doesn’t apply. Muslim reticence concerning dogs is perhaps due to the fact that rabies has always been endemic in the Middle East.",
      },
      {
        fact: "The Mayans and Aztecs symbolized every tenth day with the dog, and those born under this sign were believed to have outstanding leadership skills.",
      },
      {
        fact: "The ancient Mbaya Indians of the Gran Chaco in South America believed that humans originally lived underground until dogs dug them up.",
      },
      { fact: 'Plato once said that "a dog has the soul of a philosopher." ' },
      {
        fact: 'French poodles did not originate in France but in Germany "poodle" comes from the German pudel or pudelhund, meaning "splashing dog". Some scholars speculate the poodle’s puffs of hair evolved when hunters shaved the poodle for more efficient swimming, while leaving the pom-poms around the major joints to keep them warm.',
      },
      {
        fact: "The name of the dog on the Cracker Jacks box is Bingo. The Taco Bell Chihuahua is a rescued dog named Gidget.",
      },
      {
        fact: "The first dogs were self-domesticated wolves which, at least 12,000 years ago, became attracted to the first sites of permanent human habitation.",
      },
      { fact: "Dachshunds were bred to fight badgers in their dens." },
      {
        fact: "Laika, a Russian stray, was the first living mammal to orbit the Earth, in the Soviet Sputnik spacecraft in 1957. Though she died in space, her daughter Pushnika had four puppies with President John F. Kennedy’s terrier, Charlie.",
      },
      { fact: "Dalmatians are completely white at birth." },
      {
        fact: 'The term "dog days of summer" was coined by the ancient Greeks and Romans to describe the hottest days of summer that coincided with the rising of the Dog Star, Sirius.',
      },
      {
        fact: "Alexander the Great is said to have founded and named a city Peritas, in memory of his dog.",
      },
      {
        fact: 'In ancient Greece, kennels of dogs were kept at the sanctuary of Asclepius at Epidaurus. Dogs were frequently sacrificed there because they were plentiful, inexpensive, and easy to control. During the July 25 celebration of the kunophontis "the massacre of dogs", dog sacrifices were performed to appease the ancestors of Apollo’s son, Linos, who was devoured by dogs..',
      },
      {
        fact: "Dog trainers in ancient China were held in high esteem. A great deal of dog domestication also took place in China, especially dwarfing and miniaturization.",
      },
      {
        fact: "The ancient religion Zoroastrianism includes in its religious text titled the Zend Avesta a section devoted to the care and breeding of dogs.",
      },
      {
        fact: "The earliest European images of dogs are found in cave paintings dating back 12,000 years ago in Spain.",
      },
      {
        fact: "The dog was frequently depicted in Greek art, including Cerberus, the three-headed hound guarding the entrance to the underworld, and the hunting dogs which accompanied the virgin goddess of the chase, Diana.",
      },
      {
        fact: "During the Renaissance, detailed portraits of the dog as a symbol of fidelity and loyalty appeared in mythological, allegorical, and religious art throughout Europe, including works by Leonardo da Vinci, Diego Velázquez, Jan van Eyck, and Albrecht Durer.",
      },
      { fact: "A puppy is born blind, deaf, and toothless." },
      { fact: "The Basenji is the world’s only barkless dog." },
      {
        fact: "A dog most likely interprets a smiling person as baring their teeth, which is an act of aggression.",
      },
      {
        fact: 'The origin of amputating a dog’s tail may go back to the Roman writer Lucius Columella’s "A.D. 4-70"} assertion that tail docking prevented rabies. ',
      },
      {
        fact: 'One of Shakespeare’s most mischievous characters is Crab, the dog belonging to Launce in the Two Gentlemen of Verona. The word "watchdog" is first found in The Tempest.',
      },
      {
        fact: "President Franklin Roosevelt created a minor international incident when he claimed he sent a destroyer to the Aleutian Islands just to pick up his Scottish Terrier, Fala, who had been left behind.",
      },
      {
        fact: "Within hours of the September 11, 2001, attack on the World Trade Center, specially trained dogs were on the scene, including German Shepherds, Labs, and even a few little Dachshunds.",
      },
      {
        fact: "It costs approximately $10,000 to train a federally certified search and rescue dog.",
      },
      {
        fact: 'The smallest dog on record was a matchbox-size Yorkshire Terrier. It was 2.5" tall at the shoulder, 3.5" from nose tip to tail, and weighed only 4 ounces.',
      },
      {
        fact: "Hollywood’s first and arguably best canine superstar was Rin Tin Tin, a five-day-old German Shepherd found wounded in battle in WWI France and adopted by an American soldier, Lee Duncan. He would sign his own contracts with his paw print.",
      },
      {
        fact: "At the end of WWI, the German government trained the first guide dogs for war-blinded soldiers.",
      },
      {
        fact: "A dog can locate the source of a sound in 1/600 of a second and can hear sounds four times farther away than a human can.",
      },
      {
        fact: "Touch is the first sense the dog develops. The entire body, including the paws, is covered with touch-sensitive nerve endings.",
      },
      { fact: "Eighteen muscles or more can move a dog’s ear." },
      {
        fact: "The names of 77 ancient Egyptian dogs have been recorded. The names refer to color and character, such as Blackie, Ebony, Good Herdsman, Reliable, and Brave One.",
      },
      {
        fact: "In Egypt, a person bitten by a rabid dog was encouraged to eat the roasted liver of a dog infected with rabies to avoid contracting the disease. The tooth of a dog infected with rabies would also be put in a band tied to the arm of the person bitten. The menstrual blood of a female dog was used for hair removal, while dog genitals were used for preventing the whitening of hair.",
      },
      {
        fact: "In early Christian tradition, Saint Christopher, the patron saint of travelers, is sometimes depicted with a dog’s head.",
      },
      {
        fact: "The oldest known dog bones were found in Asia and date as far back as 10,000 B.C. The first identifiable dog breed appeared about 9000 B.C. and was probably a type of Greyhound dog used for hunting.",
      },
      { fact: "There are an estimated 400 million dogs in the world." },
      {
        fact: "The U.S. has the highest dog population in the world. France has the second highest.",
      },
      {
        fact: "Dog nose prints are as unique as human finger prints and can be used to identify them.",
      },
      {
        fact: "Bloodhound dogs have a keen sense of smell and have been used since the Middle Ages to track criminals.",
      },
      {
        fact: "It is much easier for dogs to learn spoken commands if they are given in conjunction with hand signals or gestures.",
      },
      {
        fact: "Dogs in a pack are more likely to chase and hunt than a single dog on its own. Two dogs are enough to form a pack.",
      },
      {
        fact: "Dogs can see in color, though they most likely see colors similar to a color-blind human. They can see better when the light is low.",
      },
      { fact: "Petting dogs is proven to lower blood pressure of dog owners." },
      {
        fact: "Dogs have lived with humans for over 14,000 years. Cats have lived with people for only 7,000 years.",
      },
      {
        fact: 'Zorba, an English mastiff, is the biggest dog ever recorded. He weighed 343 pounds and measured 8’ 3" from his nose to his tail.',
      },
      {
        fact: "The average dog can run about 19 mph. Greyhounds are the fastest dogs on Earth and can run at speeds of 45 mph.",
      },
      {
        fact: "One female dog and her female children could produce 4,372 puppies in seven years.",
      },
      {
        fact: "The most popular dog breed in Canada, U.S., and Great Britain is the Labrador retriever.",
      },
      {
        fact: 'Greyhounds appear to be the most ancient dog breed. "Greyhound" comes from a mistake in translating the early German name Greishund, which means "old" or "ancient dog" not from the color gray.',
      },
      {
        fact: "The oldest dog on record was an Australian cattle dog named Bluey who lived 29 years and 5 months. In human years, that is more than 160 years old.",
      },
      {
        fact: "Most experts believe humans domesticated dogs before donkeys, horses, sheep, goats, cattle, cats, or chickens.",
      },
      {
        fact: "A person standing still 300 yards away is almost invisible to a dog. But a dog can easily identify its owner standing a mile away if the owner is waving his arms.",
      },
      {
        fact: 'Dogs with big, square heads and large ears "like the Saint Bernard"} are the best at hearing subsonic sounds.',
      },
      {
        fact: "Dogs can smell about 1,000 times better than humans. While humans have 5 million smell-detecting cells, dogs have more than 220 million. The part of the brain that interprets smell is also four times larger in dogs than in humans.",
      },
      {
        fact: "Some dogs can smell dead bodies under water, where termites are hiding, and natural gas buried under 40 feet of dirt. They can even detect cancer that is too small to be detected by a doctor and can find lung cancer by sniffing a person’s breath.",
      },
      {
        fact: "Dogs have a wet nose to collect more of the tiny droplets of smelling chemicals in the air.",
      },
      {
        fact: "Dogs like sweets a lot more than cats do. While cats have around only 473 taste buds, dogs have about 1,700 taste buds. Humans have approximately 9,000.",
      },
      {
        fact: "Different smells in the a dog’s urine can tell other dogs whether the dog leaving the message is female or male, old or young, sick or healthy, happy or angry.",
      },
      {
        fact: "Male dogs will raise their legs while urinating to aim higher on a tree or lamppost because they want to leave a message that they are tall and intimidating. Some wild dogs in Africa try to run up tree trunks while they are urinating to appear to be very large.",
      },
      {
        fact: "In Croatia, scientists discovered that lampposts were falling down because a chemical in the urine of male dogs was rotting the metal.",
      },
      {
        fact: "Dogs are about as smart as a two- or three-year-old child. This means they can understand about 150-200 words, including signals and hand movements with the same meaning as words.",
      },
      {
        fact: "Countess Karlotta Libenstein of Germany left approximately $106 million to her Alsatin, Gunther III, when she died in 1992.",
      },
      {
        fact: "A lost Dachshund was found swallowed whole in the stomach of a giant catfish in Berlin on July 2003.",
      },
      {
        fact: "In Australia, a man who was arrested for drug possession argued his civil rights were violated when the drug-sniffing dog nuzzled his crotch. While the judge dismissed the charges, they were later reinstated when a prosecutor pointed out that in the animal kingdom, crotch nuzzling was a friendly gesture.",
      },
      {
        fact: 'The Beagle came into prominence in the 1300s and 1400s during the days of King Henry VII of England. Elizabeth I was fond of Pocket Beagles, which were only 9" high.',
      },
      {
        fact: "The best dog to reportedly attract a date is the Golden Retriever. The worst is the Pit Bull.",
      },
      {
        fact: 'The Akita is one of the most challenging dogs to own. Some insurance companies have even characterized it as the #1 "bad dog" and may even raise an Akita owner’s homeowner insurance costs.',
      },
      {
        fact: "The Beagle and Collie are the nosiest dogs, while the Akbash Dog and the Basenji are the quietest.",
      },
      {
        fact: "One survey reports that 33 of dog owners admit they talk to their dogs on the phone or leave messages on answering machines while they are away..",
      },
      {
        fact: "Thirty percent of all Dalmatians are deaf in one or both ears. Because bulldogs have extremely short muzzles, many spend their lives fighting suffocation. Because Chihuahuas have such small skulls, the flow of spinal fluid can be restricted, causing hydrocephalus, a swelling of the brain.",
      },
      {
        fact: "The grief suffered after a pet dog dies can be the same as that experienced after the death of a person.",
      },
      {
        fact: "There are almost 5 million dog bites per year; children are the main victims. Dog bites cause losses of over $1 billion a year.",
      },
      {
        fact: "A person should never kick a dog facing him or her. Some dogs can bite 10 times before a human can respond.",
      },
      {
        fact: "The most intelligent dogs are reportedly the Border Collie and the Poodle, while the least intelligent dogs are the Afghan Hound and the Basenji.",
      },
      {
        fact: 'One kind of Pekingese is referred to as a "sleeve" because it was bred to fit into a Chinese empress’ sleeves, which was how it was often carried around.',
      },
      {
        fact: "Is it a duck... or a dog? The Newfoundland breed has a water resistant coat and webbed feet. This dog was originally bred to help haul nets for fishermen and rescuing people at risk of drowning.",
      },
      {
        fact: 'It pays to be a lap dog. Three dogs "from First Class cabins!" survived the sinking of the Titanic – two Pomeranians and one Pekingese.',
      },
      {
        fact: 'A Beatles hit. It’s rumored that, at the end of the Beatles song, "A Day in the Life," Paul McCartney recorded an ultrasonic whistle, audible only to dogs, just for his Shetland sheepdog.',
      },
      {
        fact: "Wow, check out those choppers! Puppies have 28 teeth and normal adult dogs have 42.",
      },
      {
        fact: "Chase that tail! Dogs chase their tails for a variety of reasons: curiosity, exercise, anxiety, predatory instinct or, they might have fleas! If your dog is chasing his tail excessively, talk with your vet.",
      },
      {
        fact: "Seeing spots? Or not...  Dalmatian puppies are pure white when they are born and develop their spots as they grow older.",
      },
      {
        fact: 'Dogs do dream! Dogs and humans have the same type of slow wave sleep "SWS"} and rapid eye movement "REM" and during this REM stage dogs can dream. The twitching and paw movements that occur during their sleep are signs that your pet is dreaming',
      },
      {
        fact: "No night vision goggles needed! Dogs’ eyes contain a special membrane, called the tapetum lucidum, which allows them to see in the dark.",
      },
      {
        fact: "Pitter patter. A large breed dog’s resting heart beats between 60 and 100 times per minute, and a small dog breed’s heart beats between 100-140. Comparatively, a resting human heart beats 60-100 times per minute.",
      },
      {
        fact: "If your dog’s acting funny, get out the umbrella! According to a Petside.com/Associated Press poll, 72 of dog owners believe their dog can detect when stormy weather is on the way.",
      },
      {
        fact: "It’s not a fever... A dog’s normal temperature is between 101 and 102.5 degrees Fahrenheit. How much do you know about dog health? Take our Doggy First Aid Quiz!",
      },
      {
        fact: "Is something wet? Unlike humans who sweat everywhere, dogs only sweat through the pads of their feet.",
      },
      {
        fact: 'Here’s looking at you. Dogs have three eyelids, an upper lid, a lower lid and the third lid, called a nictitating membrane or "haw," which helps keep the eye moist and protected.',
      },
      {
        fact: "Americans love dogs! 44 of U.S. households have a dog, which equates to 55.3 million homes",
      },
      {
        fact: 'Move over Rover! 45 of dogs sleep in their owner’s bed "we’re pretty sure a large percentage also hog the blankets!" ',
      },
      {
        fact: "Why are dogs’ noses so wet? Dogs’ noses secrete a thin layer of mucous that helps them absorb scent. They then lick their noses to sample the scent through their mouth.",
      },
      {
        fact: "Yummy! Dogs have about 1,700 taste buds. Humans have approximately 9,000 and cats have around 473.",
      },
      {
        fact: "Watch that plate of cookies! A Dog’s sense of smell is 10,000 – 100,000 times more acute as that of humans.",
      },
      {
        fact: "It’s not so black and white. It’s a myth that dogs only see in black and white. In fact, it’s believed that dogs see primarily in blue, greenish-yellow, yellow and various shades of gray.",
      },
      {
        fact: 'Did you hear that? Sound frequency is measured in Hertz "Hz"}. The higher the Hertz, the higher-pitched the sound. Dogs hear best at 8,000 Hz, while humans hear best at around 2,000 Hz.',
      },
      {
        fact: "Express yourself. Dogs’ ears are extremely expressive. It’s no wonder! There are more than a dozen separate muscles that control a dog’s ear movements.",
      },
      {
        fact: "Growing up. While the Chow Chow dogs are well known for their distinctive blue-black tongues, they’re actually born with pink tongues. They turn blue-black at 8-10 weeks of age.",
      },
      {
        fact: "Why do they do that? When dogs kick after going to the bathroom, they are using the scent glands on their paws to further mark their territory.",
      },
    ],
    randomFact: Math.floor(Math.random() * 100) + 1,
  }),

  created() {
    this.takePulse(false);
  },

  computed: {
    avg() {
      const sum = this.heartbeats.reduce((acc, cur) => acc + cur, 0);
      const length = this.heartbeats.length;

      if (!sum && !length) return 0;

      return Math.ceil(sum / length);
    },
  },

  components: {
    //
  },

  methods: {
    randomGen() {
      this.randomFact = Math.floor(Math.random() * 100) + 1;
    },
    heartbeat() {
      return Math.ceil(Math.random() * (120 - 80) + 80);
    },
    async takePulse(inhale = true) {
      this.checking = true;

      inhale && (await exhale(1000));

      this.heartbeats = Array.from({ length: 20 }, this.heartbeat);

      this.checking = false;
    },
  },
};
</script>
