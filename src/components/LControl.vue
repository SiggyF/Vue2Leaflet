<script>
import propsBinder from '../utils/propsBinder.js';

const props = {
  position: {
    type: String,
    default: 'topright'
  },
  options: {
    type: Object,
    default: () => ({}),
  },
};

export default {
  name: 'LControl',
  props: props,
  mounted() {
    const options = this.options;
    const otherPropertytoInitialize = [ "position" ];
    for (var i = 0; i < otherPropertytoInitialize.length; i++) {
      const propName = otherPropertytoInitialize[i];
      if(this[propName] !== undefined) {
        options[propName] = this[propName];
      }
    }
    this.mapObject = L.control(options);
    propsBinder(this, this.mapObject, props);
    this.mapObject.addTo(this.$parent.mapObject);
  },
  methods: {
    getPosition() {
      return this.position
    },
    setPosition(position) {
      this.position = position
    },
    getContainer() {
      return this.mapObject.getContainer()
    }
    // two methods are not implemented
    // addTo is implemented by mounting and remove is implemented by destroying
  },
  beforeDestroy() {
    this.mapObject.remove();
  },
  render() {
    return null;
  }
};
</script>
