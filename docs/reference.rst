Reference
=========

The ``BrachioGraph`` class
---------------------------

::

    class BrachioGraph:

      def __init__(
          self,
          inner_arm,
          outer_arm,
          bounds=None,
          servo_1_zero=1500,
          servo_2_zero=1500,
          servo_1_angle_pws=[],
          servo_2_angle_pws=[],
          pw_up=1500,
          pw_down=1100,
      ):

* ``inner_arm``, ``outer_arm`` need to be measured from the actual plotter. They don't need to be equal, but some
  combinations are uselessly restrictive. Use the ``turtle_draw.py`` script to :ref:`see how different geometries
  affect the plottable area <visualise-area>`.
* ``bounds`` needs to be determined empirically. Or possibly, `computed
  <https://math.stackexchange.com/questions/3293200/how-can-i-calculate-the-area-reachable-by-the-tip-of-an-articulated-
  arm#comment6773872_3293200>`_.
* ``servo_1_zero`` and ``servo_2_zero``: the pulse-width at which each servo arm is exactly on the plotting grid's x
  or y axis. Ignored if the following arguments are provided.
* ``servo_1_angle_pws`` and ``servo_2_angle_pws``: lists of pulse-width/angle pairs. If provided, then
  :ref:`numpy.polyfit <polyfit>` will be used to produce a function for calculating required pulse-widths. If not, a
  more naive formula will be used.
* ``pw_up`` and ``pw_down``: pulse width values at which the pen is up/down. It makes more sense to attach the lifting
  servo horn at a different angle than to change these.


The ``linedraw`` library
------------------------

.. _vectorise:

``vectorise()``
~~~~~~~~~~~~~~~

::

    def vectorise(
        image_filename,
        resolution=1024,
        draw_hatch=True,
        hatch_size = 16,
        draw_contours=True,
        contour_simplify=1,
        ):

* ``image_filename``:  all images are expected to be found in the ``images`` directory
* ``resolution``: the number of points that will be processed across the largest dimension of the image - larger is
  more detailed, but slower - and you're unlikely to find that the resolution of the plotter itself merits increasing
  this value
* ``draw_hatch``: should the vectorisation attempt to hatch (shade) the processed image?
* ``hatch_size``: smaller is more detailed, and slower
* ``draw_contours``: find and draw outlines
* ``contour_simplify``: smaller is more detailed, and slower

It's worth experimenting with these values. Note that ``hatch_size`` and ``contour_simplify`` can be less than 1.

``vectorise`` returns a list of ``lines``, each of which is a list of points. It also creates an SVG file at ``images/<image_filename>.svg``, to give you an idea of the vectorised version.


``image_to_json()``
~~~~~~~~~~~~~~~~~~~

``image_to_json()`` takes the same parameters, but saves the result as a JSON file.

``image_to_json("africa.jpg")`` will save a file at ``images/africa.jpg.json`` (and also creates an SVG file, at ``images/africa.jpg.svg``).
