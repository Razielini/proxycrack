<template>
  <v-row
    class="d-flex justify-space-around flex-column flex-md-row align-center"
  >
    <v-col
      class=""
    >
      <v-expansion-panels
        v-model="panel"
        accordion
        class="mb-0 fontin-smallcaps divination--text"
      >
        <v-expansion-panel
          class="pa-0 ma-0"
        >
          <v-expansion-panel-header
            hide-actions
            class="title-bench text-center"
          >
            <template v-slot:default="{ open }">
              <p
                class="text-center ma-0 divination--text poe-title"
              >
                - Divination Bench -
              </p>
            </template>
          </v-expansion-panel-header>
          <v-expansion-panel-content
            class="pa-0 ma-0"
          >
            <v-row
              class="md-flex justify-md-space-between align-center pa-4 ma-0 item-bench"
            >
              <img
                :src="ui.bullet"
              >
              <label
                class="divination--text flex-grow poe-title mx-4 md-col-3"
              >
                Title
              </label>
              <v-flex
                md6
                sm12
              >
                <input
                  v-model="divination.title"
                  :placeholder="divination.title"
                  class="divination--text pa-2 flex-grow mt-0"
                  style="width: 100%"
                >
              </v-flex>
            </v-row>
            <v-row
              class="md-flex justify-md-space-between align-center pa-4 ma-0 item-bench"
            >
              <img
                :src="ui.bullet"
              >
              <label
                class="divination--text flex-grow mx-4 poe-title"
              >
                Reward
              </label>
              <v-flex
                md6
                sm12
              >
                <input
                  v-model="divination.reward"
                  placeholder="Write a reward"
                  class="divination--text pa-2 flex-grow mt-0"
                  style="width: 100%"
                >
              </v-flex>
            </v-row>
            <v-row
              class="md-flex justify-md-space-between align-center pa-4 ma-0 item-bench"
            >
              <img
                :src="ui.bullet"
              >
              <label
                class="divination--text flex-grow mx-4 poe-title"
              >
                Stack
              </label>
              <v-flex
                md6
                sm12
              >
                <input
                  v-model="divination.stack"
                  :placeholder="divination.stack"
                  type="number"
                  step="1"
                  class="divination--text pa-2 flex-grow mt-0"
                  style="width: 100%"
                >
              </v-flex>
            </v-row>
            <div
              class="item-bench tw-justify-between tw-flex-col tw-flex pa-4"
            >
              <label
                class="tw-block tw-text-sm tw-leading-5 tw-text-xl tw-font-medium mt-2"
              >
                Lore
              </label>
              <v-textarea
                v-model="divination.lore"
                color="divination"
                counter
                class="px-0 ma-0"
              />
            </div>
          </v-expansion-panel-content>
        </v-expansion-panel>
        <v-expansion-panel
          class="pa-0 ma-0"
        >
          <v-expansion-panel-header
            hide-actions
            class="title-bench"
          >
            <template v-slot:default="{ open }">
              <p
                class="text-center ma-0 poe-title"
              >
                - Images -
              </p>
            </template>
          </v-expansion-panel-header>
          <v-expansion-panel-content
            class="pa-0 ma-0"
          >
            <v-row
              class="col-12 ma-0"
            >
              <v-spacer />
              <p
                class="fontin-smallcaps cursor-pointer mx-2 my-0 hover-item"
                @click="lessPage()"
              >
                &#060; Prev
              </p>
              <p
                class="fontin-smallcaps mx-2 my-0"
              >
                {{ pagination.page }} / {{ totalPages }}
              </p>
              <p
                class="fontin-smallcaps cursor-pointer mx-2 my-0 hover-item"
                @click="addPage()"
              >
                Next &#62;
              </p>
            </v-row>
            <v-data-iterator
              :items="divinationImages"
              :items-per-page.sync="pagination.itemsPerPage"
              :page="pagination.page"
              hide-default-footer
            >
              <template v-slot:default="props">
                <div
                  class="fluid grid-list-md col-12 flex-wrap"
                >
                  <v-layout
                    align-start
                    justify-start
                    fill-height
                    flex-wrap
                    row
                  >
                    <v-flex
                      v-for="item in props.items"
                      :key="item.src"
                      md4
                      sm6
                      :class="activeImage(item.src) + ' card-image pa-2 pt-1 cursor-pointer md4 xs6'"
                      @click="imageSelected(item)"
                    >
                      <v-img
                        :src="'/poe/divination/img/' + item.src"
                      />
                    </v-flex>
                  </v-layout>
                </div>
              </template>
            </v-data-iterator>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>

      <div
        class="item-bench justify-space-between flex-column d-flex fontin-smallcaps"
      >
        <button
          type="button"
          class="pa-5"
          :disabled="createCard"
          @click="saveIMG()"
        >
          {{ createCard ? 'Creating Card....' : 'Download Card' }}
        </button>
      </div>
    </v-col>
    <v-col
      class="pa-0 ma-0 mx-auto"
    >
      <div
        id="wrapper-divination-card"
        :style="'background-image: url(/poe/divination/img/' + divination.img +'); background-size: ' + bgSizeImage($vuetify.breakpoint.xs) + 'px; background-position-y: ' + bgPosYImage($vuetify.breakpoint.xs) + 'px;'"
        class="bg-no-repeat mx-auto mt-0 fontin-smallcaps"
      >
        <div
          class="d-flex flex-column align-center frame-divination-card"
        >
          <div
            class="poe-title text-divination-title text-center black--text"
            :style="'margin-top:' + marginTop($vuetify.breakpoint.xs, 'title') + 'px;'"
          >
            {{ divination.title }}
          </div>
          <div
            class="align-self-start white--text divinationcard--text font-size-larger"
            :style="'margin-top:' + marginTop($vuetify.breakpoint.xs, 'stack') + 'px; margin-left: ' + marginLeftStack($vuetify.breakpoint.xs) + 'px;'"
          >
            {{ divination.stack }}
          </div>
          <div
            class="text-divination-reward text-center divinationcard--text font-size-x-large"
            :style="'margin-top:' + marginTop($vuetify.breakpoint.xs, 'reward') + 'px;'"
          >
            {{ divination.reward }}
          </div>
          <div
            class="text-divination-reward text-center divinationcard--text lore"
            :style="'margin-top:' + marginTop($vuetify.breakpoint.xs, 'lore') + 'px;'"
          >
            {{ divination.lore }}
          </div>
        </div>
      </div>
    </v-col>
  </v-row>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'
const htmlToImage = require('html-to-image')
const download = require('downloadjs')

@Component
export default class ViewPoeDivination extends Vue {
  divinationImages: any[] = this.$store.state.poeDivination.images
  ui: any = {
    bullet: this.$store.state.poeDivination.ui.bullet
  }

  pagination: any = {
    page: 1,
    itemsPerPage: 9
  }

  isHydrated: boolean = false

  createCard: boolean = false

  panel: number = 0

  divination: any = {
    title: 'Alone in the Darkness',
    stack: '6',
    reward: 'Delve Item',
    lore: 'Sometimes, the most beautiful treasures...are the ones you cannot have. - Beryl, Survivor from the Azurite Mines',
    img: 'Alone_in_the_Darkness_card_art.png'
  }

  activeImage (src: string) {
    let res: string = ''
    if (src === this.divination.img) {
      res = 'card-image-active'
    }
    return res
  }

  bgSizeImage (breakpoint: boolean) {
    let res: number = 400
    if (breakpoint) {
      res = 330
    }
    return res
  }

  marginTop (breakpoint: boolean, element: string) {
    let res: number = 0
    if (element === 'title') {
      res = 20
      if (breakpoint) {
        res = 65
      }
    } else if (element === 'stack') {
      res = 263
      if (breakpoint) {
        res = 220
      }
    } else if (element === 'reward') {
      res = 55
      if (breakpoint) {
        res = 35
      }
    } else if (element === 'lore') {
      res = 45
      if (breakpoint) {
        res = 45
      }
    }
    return res
  }

  marginLeftStack (breakpoint: boolean) {
    let res: number = 118

    if (breakpoint) {
      res = 58
    }

    res = res - ((this.divination.stack.length - 1) * 4)
    return res
  }

  bgPosYImage (breakpoint: boolean) {
    let res: number = 55
    if (breakpoint) {
      res = 97
    }
    return res
  }

  get totalPages () {
    return Math.ceil(Math.trunc(this.divinationImages.length / this.pagination.itemsPerPage))
  }

  mounted () {
    console.info('mounted :: modal-images')
  }

  imageSelected (item: any) {
    this.divination.img = item.src
    item.selected = true
  }

  divinationPaginated () {
    const images = [...this.divinationImages]
    const itemsPerPage: number = this.pagination.itemsPerPage
    const initial: number = ((this.pagination.page - 1) * itemsPerPage)
    console.log('images :: ', images)
    console.log('initial :: ', initial)
    const slice = images.slice(initial, initial + itemsPerPage)
    console.log('slice :: ', slice)
    return images.slice(initial, initial + itemsPerPage)
  }

  saveIMG () {
    console.log('saveIMG')
    this.createCard = true
    htmlToImage.toPng(document.getElementById('wrapper-divination-card'))
      .then((dataUrl: any) => {
        let img = new Image()
        img.src = dataUrl
        // this.printTitle('Hello')
        download(dataUrl, this.toSlug(this.divination.title) + '.png')
        console.log('saveIMG img ::', img)
      })
      .catch((error: any) => {
        console.error('oops, something went wrong!', error)
      })
      .finally(() => {
        this.createCard = false
      })
  }

  toSlug (str: string) {
    console.log('toSlug :: ', str)
    str = String(str).toString()
    str = str.replace(/^\s+|\s+$/g, '') // trim
    str = str.toLowerCase()
    // remove accents, swap ñ for n, etc
    const swaps: any = {
      '0': ['°', '₀', '۰', '０'],
      '1': ['¹', '₁', '۱', '１'],
      '2': ['²', '₂', '۲', '２'],
      '3': ['³', '₃', '۳', '３'],
      '4': ['⁴', '₄', '۴', '٤', '４'],
      '5': ['⁵', '₅', '۵', '٥', '５'],
      '6': ['⁶', '₆', '۶', '٦', '６'],
      '7': ['⁷', '₇', '۷', '７'],
      '8': ['⁸', '₈', '۸', '８'],
      '9': ['⁹', '₉', '۹', '９'],
      'a': ['à', 'á', 'ả', 'ã', 'ạ', 'ă', 'ắ', 'ằ', 'ẳ', 'ẵ', 'ặ', 'â', 'ấ', 'ầ', 'ẩ', 'ẫ', 'ậ', 'ā', 'ą', 'å', 'α', 'ά', 'ἀ', 'ἁ', 'ἂ', 'ἃ', 'ἄ', 'ἅ', 'ἆ', 'ἇ', 'ᾀ', 'ᾁ', 'ᾂ', 'ᾃ', 'ᾄ', 'ᾅ', 'ᾆ', 'ᾇ', 'ὰ', 'ά', 'ᾰ', 'ᾱ', 'ᾲ', 'ᾳ', 'ᾴ', 'ᾶ', 'ᾷ', 'а', 'أ', 'အ', 'ာ', 'ါ', 'ǻ', 'ǎ', 'ª', 'ა', 'अ', 'ا', 'ａ', 'ä'],
      'b': ['б', 'β', 'ب', 'ဗ', 'ბ', 'ｂ'],
      'c': ['ç', 'ć', 'č', 'ĉ', 'ċ', 'ｃ'],
      'd': ['ď', 'ð', 'đ', 'ƌ', 'ȡ', 'ɖ', 'ɗ', 'ᵭ', 'ᶁ', 'ᶑ', 'д', 'δ', 'د', 'ض', 'ဍ', 'ဒ', 'დ', 'ｄ'],
      'e': ['é', 'è', 'ẻ', 'ẽ', 'ẹ', 'ê', 'ế', 'ề', 'ể', 'ễ', 'ệ', 'ë', 'ē', 'ę', 'ě', 'ĕ', 'ė', 'ε', 'έ', 'ἐ', 'ἑ', 'ἒ', 'ἓ', 'ἔ', 'ἕ', 'ὲ', 'έ', 'е', 'ё', 'э', 'є', 'ə', 'ဧ', 'ေ', 'ဲ', 'ე', 'ए', 'إ', 'ئ', 'ｅ'],
      'f': ['ф', 'φ', 'ف', 'ƒ', 'ფ', 'ｆ'],
      'g': ['ĝ', 'ğ', 'ġ', 'ģ', 'г', 'ґ', 'γ', 'ဂ', 'გ', 'گ', 'ｇ'],
      'h': ['ĥ', 'ħ', 'η', 'ή', 'ح', 'ه', 'ဟ', 'ှ', 'ჰ', 'ｈ'],
      'i': ['í', 'ì', 'ỉ', 'ĩ', 'ị', 'î', 'ï', 'ī', 'ĭ', 'į', 'ı', 'ι', 'ί', 'ϊ', 'ΐ', 'ἰ', 'ἱ', 'ἲ', 'ἳ', 'ἴ', 'ἵ', 'ἶ', 'ἷ', 'ὶ', 'ί', 'ῐ', 'ῑ', 'ῒ', 'ΐ', 'ῖ', 'ῗ', 'і', 'ї', 'и', 'ဣ', 'ိ', 'ီ', 'ည်', 'ǐ', 'ი', 'इ', 'ی', 'ｉ'],
      'j': ['ĵ', 'ј', 'Ј', 'ჯ', 'ج', 'ｊ'],
      'k': ['ķ', 'ĸ', 'к', 'κ', 'Ķ', 'ق', 'ك', 'က', 'კ', 'ქ', 'ک', 'ｋ'],
      'l': ['ł', 'ľ', 'ĺ', 'ļ', 'ŀ', 'л', 'λ', 'ل', 'လ', 'ლ', 'ｌ'],
      'm': ['м', 'μ', 'م', 'မ', 'მ', 'ｍ'],
      'n': ['ñ', 'ń', 'ň', 'ņ', 'ŉ', 'ŋ', 'ν', 'н', 'ن', 'န', 'ნ', 'ｎ'],
      'o': ['ó', 'ò', 'ỏ', 'õ', 'ọ', 'ô', 'ố', 'ồ', 'ổ', 'ỗ', 'ộ', 'ơ', 'ớ', 'ờ', 'ở', 'ỡ', 'ợ', 'ø', 'ō', 'ő', 'ŏ', 'ο', 'ὀ', 'ὁ', 'ὂ', 'ὃ', 'ὄ', 'ὅ', 'ὸ', 'ό', 'о', 'و', 'θ', 'ို', 'ǒ', 'ǿ', 'º', 'ო', 'ओ', 'ｏ', 'ö'],
      'p': ['п', 'π', 'ပ', 'პ', 'پ', 'ｐ'],
      'q': ['ყ', 'ｑ'],
      'r': ['ŕ', 'ř', 'ŗ', 'р', 'ρ', 'ر', 'რ', 'ｒ'],
      's': ['ś', 'š', 'ş', 'с', 'σ', 'ș', 'ς', 'س', 'ص', 'စ', 'ſ', 'ს', 'ｓ'],
      't': ['ť', 'ţ', 'т', 'τ', 'ț', 'ت', 'ط', 'ဋ', 'တ', 'ŧ', 'თ', 'ტ', 'ｔ'],
      'u': ['ú', 'ù', 'ủ', 'ũ', 'ụ', 'ư', 'ứ', 'ừ', 'ử', 'ữ', 'ự', 'û', 'ū', 'ů', 'ű', 'ŭ', 'ų', 'µ', 'у', 'ဉ', 'ု', 'ူ', 'ǔ', 'ǖ', 'ǘ', 'ǚ', 'ǜ', 'უ', 'उ', 'ｕ', 'ў', 'ü'],
      'v': ['в', 'ვ', 'ϐ', 'ｖ'],
      'w': ['ŵ', 'ω', 'ώ', 'ဝ', 'ွ', 'ｗ'],
      'x': ['χ', 'ξ', 'ｘ'],
      'y': ['ý', 'ỳ', 'ỷ', 'ỹ', 'ỵ', 'ÿ', 'ŷ', 'й', 'ы', 'υ', 'ϋ', 'ύ', 'ΰ', 'ي', 'ယ', 'ｙ'],
      'z': ['ź', 'ž', 'ż', 'з', 'ζ', 'ز', 'ဇ', 'ზ', 'ｚ'],
      'aa': ['ع', 'आ', 'آ'],
      'ae': ['æ', 'ǽ'],
      'ai': ['ऐ'],
      'ch': ['ч', 'ჩ', 'ჭ', 'چ'],
      'dj': ['ђ', 'đ'],
      'dz': ['џ', 'ძ'],
      'ei': ['ऍ'],
      'gh': ['غ', 'ღ'],
      'ii': ['ई'],
      'ij': ['ĳ'],
      'kh': ['х', 'خ', 'ხ'],
      'lj': ['љ'],
      'nj': ['њ'],
      'oe': ['ö', 'œ', 'ؤ'],
      'oi': ['ऑ'],
      'oii': ['ऒ'],
      'ps': ['ψ'],
      'sh': ['ш', 'შ', 'ش'],
      'shch': ['щ'],
      'ss': ['ß'],
      'sx': ['ŝ'],
      'th': ['þ', 'ϑ', 'ث', 'ذ', 'ظ'],
      'ts': ['ц', 'ც', 'წ'],
      'ue': ['ü'],
      'uu': ['ऊ'],
      'ya': ['я'],
      'yu': ['ю'],
      'zh': ['ж', 'ჟ', 'ژ'],
      '(c)': ['©'],
      'A': ['Á', 'À', 'Ả', 'Ã', 'Ạ', 'Ă', 'Ắ', 'Ằ', 'Ẳ', 'Ẵ', 'Ặ', 'Â', 'Ấ', 'Ầ', 'Ẩ', 'Ẫ', 'Ậ', 'Å', 'Ā', 'Ą', 'Α', 'Ά', 'Ἀ', 'Ἁ', 'Ἂ', 'Ἃ', 'Ἄ', 'Ἅ', 'Ἆ', 'Ἇ', 'ᾈ', 'ᾉ', 'ᾊ', 'ᾋ', 'ᾌ', 'ᾍ', 'ᾎ', 'ᾏ', 'Ᾰ', 'Ᾱ', 'Ὰ', 'Ά', 'ᾼ', 'А', 'Ǻ', 'Ǎ', 'Ａ', 'Ä'],
      'B': ['Б', 'Β', 'ब', 'Ｂ'],
      'C': ['Ç', 'Ć', 'Č', 'Ĉ', 'Ċ', 'Ｃ'],
      'D': ['Ď', 'Ð', 'Đ', 'Ɖ', 'Ɗ', 'Ƌ', 'ᴅ', 'ᴆ', 'Д', 'Δ', 'Ｄ'],
      'E': ['É', 'È', 'Ẻ', 'Ẽ', 'Ẹ', 'Ê', 'Ế', 'Ề', 'Ể', 'Ễ', 'Ệ', 'Ë', 'Ē', 'Ę', 'Ě', 'Ĕ', 'Ė', 'Ε', 'Έ', 'Ἐ', 'Ἑ', 'Ἒ', 'Ἓ', 'Ἔ', 'Ἕ', 'Έ', 'Ὲ', 'Е', 'Ё', 'Э', 'Є', 'Ə', 'Ｅ'],
      'F': ['Ф', 'Φ', 'Ｆ'],
      'G': ['Ğ', 'Ġ', 'Ģ', 'Г', 'Ґ', 'Γ', 'Ｇ'],
      'H': ['Η', 'Ή', 'Ħ', 'Ｈ'],
      'I': ['Í', 'Ì', 'Ỉ', 'Ĩ', 'Ị', 'Î', 'Ï', 'Ī', 'Ĭ', 'Į', 'İ', 'Ι', 'Ί', 'Ϊ', 'Ἰ', 'Ἱ', 'Ἳ', 'Ἴ', 'Ἵ', 'Ἶ', 'Ἷ', 'Ῐ', 'Ῑ', 'Ὶ', 'Ί', 'И', 'І', 'Ї', 'Ǐ', 'ϒ', 'Ｉ'],
      'J': ['Ｊ'],
      'K': ['К', 'Κ', 'Ｋ'],
      'L': ['Ĺ', 'Ł', 'Л', 'Λ', 'Ļ', 'Ľ', 'Ŀ', 'ल', 'Ｌ'],
      'M': ['М', 'Μ', 'Ｍ'],
      'N': ['Ń', 'Ñ', 'Ň', 'Ņ', 'Ŋ', 'Н', 'Ν', 'Ｎ'],
      'O': ['Ó', 'Ò', 'Ỏ', 'Õ', 'Ọ', 'Ô', 'Ố', 'Ồ', 'Ổ', 'Ỗ', 'Ộ', 'Ơ', 'Ớ', 'Ờ', 'Ở', 'Ỡ', 'Ợ', 'Ø', 'Ō', 'Ő', 'Ŏ', 'Ο', 'Ό', 'Ὀ', 'Ὁ', 'Ὂ', 'Ὃ', 'Ὄ', 'Ὅ', 'Ὸ', 'Ό', 'О', 'Θ', 'Ө', 'Ǒ', 'Ǿ', 'Ｏ', 'Ö'],
      'P': ['П', 'Π', 'Ｐ'],
      'Q': ['Ｑ'],
      'R': ['Ř', 'Ŕ', 'Р', 'Ρ', 'Ŗ', 'Ｒ'],
      'S': ['Ş', 'Ŝ', 'Ș', 'Š', 'Ś', 'С', 'Σ', 'Ｓ'],
      'T': ['Ť', 'Ţ', 'Ŧ', 'Ț', 'Т', 'Τ', 'Ｔ'],
      'U': ['Ú', 'Ù', 'Ủ', 'Ũ', 'Ụ', 'Ư', 'Ứ', 'Ừ', 'Ử', 'Ữ', 'Ự', 'Û', 'Ū', 'Ů', 'Ű', 'Ŭ', 'Ų', 'У', 'Ǔ', 'Ǖ', 'Ǘ', 'Ǚ', 'Ǜ', 'Ｕ', 'Ў', 'Ü'],
      'V': ['В', 'Ｖ'],
      'W': ['Ω', 'Ώ', 'Ŵ', 'Ｗ'],
      'X': ['Χ', 'Ξ', 'Ｘ'],
      'Y': ['Ý', 'Ỳ', 'Ỷ', 'Ỹ', 'Ỵ', 'Ÿ', 'Ῠ', 'Ῡ', 'Ὺ', 'Ύ', 'Ы', 'Й', 'Υ', 'Ϋ', 'Ŷ', 'Ｙ'],
      'Z': ['Ź', 'Ž', 'Ż', 'З', 'Ζ', 'Ｚ'],
      'AE': ['Æ', 'Ǽ'],
      'Ch': ['Ч'],
      'Dj': ['Ђ'],
      'Dz': ['Џ'],
      'Gx': ['Ĝ'],
      'Hx': ['Ĥ'],
      'Ij': ['Ĳ'],
      'Jx': ['Ĵ'],
      'Kh': ['Х'],
      'Lj': ['Љ'],
      'Nj': ['Њ'],
      'Oe': ['Œ'],
      'Ps': ['Ψ'],
      'Sh': ['Ш'],
      'Shch': ['Щ'],
      'Ss': ['ẞ'],
      'Th': ['Þ'],
      'Ts': ['Ц'],
      'Ya': ['Я'],
      'Yu': ['Ю'],
      'Zh': ['Ж']
    }

    Object.keys(swaps).forEach((swap: any) => {
      swaps[swap].forEach((s: any) => {
        str = str.replace(new RegExp(s, 'g'), swap)
      })
    })

    return str
      .replace(/[^a-z0-9 -]/g, '') // remove invalid chars
      .replace(/\s+/g, '-') // collapse whitespace and replace by -
      .replace(/-+/g, '-') // collapse dashes
      .replace(/^-+/, '') // trim - from start of text
      .replace(/-+$/, '')
  }

  addPage () {
    this.pagination.page++
    if (this.pagination.page > this.totalPages) {
      this.pagination.page = 1
    }
  }

  lessPage () {
    this.pagination.page--
    if (this.pagination.page <= 0) {
      this.pagination.page = this.totalPages
    }
  }
}
</script>

<style>
  /* Sample `apply` at-rules with Tailwind CSS
  .container {
    @apply min-h-screen flex justify-center items-center text-center mx-auto;
  }
  */

  .cursor-pointer {
    cursor: pointer;
  }

  @font-face {
    font-family: 'Fontin SmallCaps';
    src: url('/poe/divination/font/Fontin-SmallCaps.ttf');
    font-weight: 400;
    font-style: italic;
  }

  .poe-title {
    font-size: 1.25rem;
  }

  .v-expansion-panel-content__wrap {
    padding: 0 !important;
  }

  #wrapper-divination-card {
    background-size: auto;
    background-position-x: center;
    background-position-y: 55px;
    max-width: 540px;
  }

  #wrapper-divination-card .lore {
    width: 300px;
  }

  .font-size-x-large {
    font-size: x-large;
  }

  .font-size-larger {
    font-size: larger;
  }

  input, textarea {
    background: black;
    border: 1px solid #88623b;
  }

  .fontin-smallcaps {
    font-family: 'Fontin SmallCaps';
  }

  .frame-divination-card {
    background-image: url('/poe/divination/divination_card_frame.png');
    background-repeat: no-repeat;
    background-position: center;
    background-size: contain;
    min-height: 668px;
    font-family: 'Fontin SmallCaps';
  }

  .title-bench {
    color: #b8905f;
    border: 1px solid #3d3f48;
    background: url(https://pvaass.github.io/poecraft/img/section-title-left.png) no-repeat left top,
    url(https://pvaass.github.io/poecraft/img/section-title-right.png) no-repeat right top #000;
    display: flex;
    align-items: center;
  }

  .item-bench textarea {
    color: #b8905f !important;
    padding: 8px;
  }

  .hover-item:hover {
    color: #b8905f;
  }

  .item-bench {
    color: #b8905f;
    border-top: 2px solid #131111;
    background-color: #211b14;
  }

  .item-bench:hover {
    background-color: #392810;
  }

  .card-image {
    filter: grayscale(100%);
  }

  .card-image:hover {
    filter: grayscale(0%);
  }

  .card-image-active {
    filter: grayscale(0%);
    border: 1px dashed;
  }

  .card-image .title {
    height: 34px;
    color: #ffff77;
    background: url(/poe/divination/ui/HeadRareLeft.png) no-repeat left top,
    url(/poe/divination/ui/HeadRareRight.png) no-repeat right top,
    url(/poe/divination/ui/HeadRareLineCenter.png) repeat-x right top;
  }
</style>
